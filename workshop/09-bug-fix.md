# Using spec driven development to fix defects

In this lab we are going to use spec driven development to do something slightly different. Tackle application defects. I have created a [sample application](https://github.com/094459/sdd-workshop-book-sharing-broken) which has some [defects](/resources/BUGS.md).

The goal of this lab is to:

* understand how to prepare for using AI coding tools like Kiro to help you resolve defects 
* show how to apply the spec driven development approach to help tackle defects
* work through the spec workflow to get your application back up and running

At the end of this lab, you will be able to apply this to your own projects and code.

---


![Lab](/images/lab-header.png)

In this first lab we are going to create a new project workspace, and check out the code from source control.

#### Lab-01


1. Open up a terminal, and run the following commands to create a new project workspace on your machine - I am going to call mine "~/kiro/sdd-bugix"

```
cd ~/kiro
mkdir ~/kiro/sdd-bugix && cd sdd-bugix
```

and then check out the demo broken application into this directory and change directory to make it your project directory

```
git clone https://github.com/094459/sdd-workshop-book-sharing-broken
cd sdd-workshop-book-sharing-broken
```

3. Launch Kiro from the command line

```
kiro .
```

---

![Lab](/images/lab-header.png)

In this lab we will now walk you through the spec workflow to identify and suggest fixes for defects. We are going to resolve this bug that the current broken application has:

* When running the application code base (book sharing app). Logged in as a user, attempting to return a book doesn't clear the current borrower

You can start the application and create a couple of test users and validate that this is indeed an issue. At the end of this lab you can try again and see if the issue has been resolved.


#### Lab-02

![Lab](/images/lab-header-end.png)

1. The first thing you will need to do when taking a spec driven approach to fixing defects is to make sure you have followed good practices around structured troubleshooting. You will need to make sure that you can clearly articulate:

* the precise issue, providing a consise sentence that summarises the key issue
* can provide the steps to reproduce the issue
* can articulate the expected behaviour (good)

Using the example bug we might phrase this as follows:

```
Returning a book doesn't clear the current borrower.

- User A lists a book
- User B requests to borrow it, User A approves
- User B returns the book
- Go to User B's "Currently Borrowed" page

Correct behaviour should clear the current borrower.
```

2. From the chat interface in Kiro, select "Spec" and then enter the following:

"Create a bugfix spec that resolves an issue with the app. Returning a book doesn't clear the current borrower.
- User A lists a book
- User B requests to borrow it, User A approves
- User B returns the book
- Go to User B's "Currently Borrowed" page
Correct behaviour should clear the current borrower."

3. The spec workflow dialog will appear. It will list "Bug Fix" and "Build a Feature" - the "Bug Fix" should be identified as recommended. Click on that and then select "Submit Answer"

This will initiate the bugfix spec workflow.

4. Watch the chat interface - Kiro will now attempt to review the code against the bug you have stated. It will start to generate a new artefact, the "bugfix.md". It should look similar to the following:

![bugfix screen](/images/bug-fix.png)

Notice that the workflow is Bugfix > Design > Tasks.

5. Review the document and notice the structure:

- Introduction - provides an overview of the defect
- Current behaviour (defect) - outlines the issue in clear and unambigious language
- Expected behavior (correct) - explains what should happen
- Unchanged behaviour (regression) - provides a set of criteria to ensure that additional tests are carried out to mitigate any regressions that might be introduced by a fix

6. Once you have reviewed the defect document, click on "Continue" > "Generate Design" - this will now begin the process of creating a design document that will outline the fix.

Once completed, review the doc. This is different to other design documents that other spec workflows produce. The key points to look at when reviewing this:

- Overview - provides a high level view of the fix design
- Bug Condition - goes into more lower level details of the issue
- Examples - provides a solid example to help explain the defect
- Expected behaviour - outlines how the code/app should work
- Root Cause - provides a suggested root cause analsyis
- Correctness Properties - add some property based testing to validate behaviour
- Fix implementation - details of the actual fix
- Testing - what tests will be implemented to validate the fix
- Regression - what regression tests are required


7. To move this to actually executing the fix, we move the workflow to the next stage. Use the "Continue" > "Generate Tasks" which will kick start the process for turning this bug fix design into an implementation plan.

When finished, review the tasks.md. Like the design.md, the format of the tasks.md will be different to other spec workflow you might have used. That said, the way you initiate the execution remains the same.

Click on "Run all tasks" to start the bug fixing process.

8. Follow the status of the fix through the chat window. You will be prompted for permissions as it starts generating the fix and supporting test code.

This can take 5-10 minutes, or longer for more complex issues.

Once completed, you should get a summary in the chat status window. This is what it should look similar too:

```
Fix applied: Added book.current_borrower_id = None in books.py
 after book.is_available = True in the return_book handler — a single-line change.

Verification:

Bug condition exploration tests confirmed the bug existed (failed on unfixed code), then passed after the fix
Preservation tests confirmed no regressions — book availability, borrowing history, approve flow, and borrowed-page queries all work correctly

Full test suite passes (2 pre-existing unrelated failures in CSV export tests remain unchanged)
The returned books will no longer appear on the borrower's "Currently Borrowed" page.
```

You can now start the application and validate that this has indeed fixed the issue. 

9. Congratulations, you have now completed the bugfix spec workflow and are ready to use this in your real projects.

---
