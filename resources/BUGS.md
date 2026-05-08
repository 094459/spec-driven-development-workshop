# Known Bugs

This document describes two subtle bugs that have been introduced into the application. Each bug allows the app to run and appear functional under normal testing, but causes failures under specific sequences of events.

---

## Bug 1: Approving a borrow request has no safety guard against self-rejection

**File:** `src/routes/books.py` — `approve_request()` function

### What changed

The `.filter(BorrowRequest.request_id != request_id)` clause was removed from the query that rejects other pending requests after an approval. The code now queries *all* pending requests for the book without excluding the just-approved one.

### How to reproduce

1. User A lists a book
2. User B submits a borrow request for the book
3. User C also submits a borrow request for the same book
4. User A approves User B's request

**Expected:** User B's request is `approved`, User C's request is `rejected`.

**What actually happens (today):** It appears to work correctly because SQLAlchemy auto-flushes the `approved` status to the database before the subsequent query runs, so the `filter_by(status='pending')` no longer matches User B's request. The bug is **latent**.

**When it breaks:**
- If anyone changes SQLAlchemy's `autoflush` setting to `False` (a common performance optimization), the approved request will still have `status='pending'` in the database at query time, and the loop will overwrite it to `rejected` — the approval silently disappears.
- If the code is reordered so the "reject others" query runs before the status is set to `approved`, the same thing happens.
- The bug removes a critical safety invariant: the code now *depends on flush timing* for correctness instead of explicitly excluding the approved request.

### Root cause

Missing exclusion filter. The query that rejects other pending requests should never be able to match the request being approved.

### Fix

Restore the exclusion filter in `approve_request()`:

```python
# Current (buggy):
other_requests = BorrowRequest.query.filter_by(
    book_id=book.book_id,
    status='pending'
).all()

# Fixed:
other_requests = BorrowRequest.query.filter_by(
    book_id=book.book_id,
    status='pending'
).filter(BorrowRequest.request_id != request_id).all()
```

---

## Bug 2: Returning a book doesn't clear the current borrower — ghost borrower

**File:** `src/routes/books.py` — `return_book()` function

### What changed

The line `book.current_borrower_id = None` was removed. When a book is returned, `is_available` is set back to `True` and the borrowing history is updated, but the `current_borrower_id` foreign key still points to the returning user.

### How to reproduce

1. User A lists a book
2. User B requests to borrow it, User A approves
3. User B returns the book
4. Go to User B's "Currently Borrowed" page (`/profile/borrowed`)

**Expected:** The page shows no books — User B has returned everything.

**Actual:** The book still appears on User B's borrowed page because `current_borrower_id` still equals User B's ID. The book shows as "available" on the public listing (since `is_available = True`), but User B's profile permanently shows a phantom borrowed book.

**Further cascade:**
- If User C now borrows the same book, `current_borrower_id` gets overwritten to User C, which *masks* the bug for User B retroactively. This makes the bug appear intermittent and very hard to track down.
- If no one else ever borrows the book, User B sees it on their borrowed page forever.
- The `/profile/view/<user_id>` page filters by `is_available=True`, so the book still appears in the owner's public profile — creating a contradictory state where a book is simultaneously "available" and "borrowed by someone."

### Root cause

The `return_book()` function sets `is_available = True` and updates the history record, but never nulls out `current_borrower_id`. The two fields fall out of sync.

### Fix

Restore the line that clears the borrower in `return_book()`:

```python
# After setting is_available and updating history, add:
book.current_borrower_id = None
```
