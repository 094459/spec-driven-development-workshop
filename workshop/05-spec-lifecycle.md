_Spec driven development is still emerging and so areas such as the spec driven development lifecycle are still evolving - bear that in mind as we explore the current approach to this_
# Lifecycle

In the previous labs you have seen what specs are and looked at several different spec workflows. What if you want to change something though? In this section we look at the typical lifecycle of specs, and how we manage change.

A spec has a lifecycle: 

* you create a spec (and then work through the steps within a workflow) 
* you update a spec (iterating through the same workflow relevant to the change being made)
* you can delete/remove specs

![lifecycle](/images/Pasted%20image%2020260507223416.png)

# Change scenarios

There are a number of scenarios where you might need or want to make changes to your specs. Each scenario will require you to approach it in slightly different ways. Lets dive into this.

## Clarification

Minor updates that do not functionally change design or implementation but might help improve precision. Some examples of this include fixing typos, formatting improvements, clearer wording.

For these kinds of trivial changes, you and adjust/amend the documents directly as they will not impact any downstream workflow changes. The exception perhaps being where those typos are reflect in artifacts that are built (e.g you wanted to create a page called "Help" but created a typo called "Welp" and now you want to change that back - this would require you to kick off a workflow refresh)

## Discoveries

During the implementation phase you might discover implementation details (tech) that lead to changes in design. This is part of the development process, and you will likely be able to recall your own examples of where you started off with a design, and then ran into issues or limitations during implementation. Examples of these kinds of changes might include:

- **Technical constraints** - During code generation you identified sub optimisation choices: limitations with libraries or APIs, performance issues, security concerns
- **Integration challenges** - Data or interface format issues, complexities with authentication and authorisation, new/updated interfaces
- **Feedback** - Testing or user feedback, which includes accessibility, mobile support, responsiveness, browser compatibility and more

For these kinds of changes we would update the design.md, and then kick off an update which we will come to in a moment.

## Changes

Probably the most straightforward change is where you want to update an existing spec (maybe add or update a requirement).

For these kinds of changes we would need to implement a full refresh of the lifecycle, which depending on what was asked, could lead to working through the workflow steps again. You will explore this during the labs, but the workflow is as different depending on which spec workflow you are using.

### Feature, requirements first

The update workflow follows these three steps:

- **Update Requirements** Either modify the requirements.md file directly or initiate a spec session and instruct Kiro to add new requirements or design elements.

- **Update Design** From the chat interface, initiate a design review by using a prompt such as "Review the design.md against changes in the requirements"

- **Sync files** Update the implementation plan by bavigating to the tasks.md file and choose Sync Files. This will create new tasks that map to the new requirements.

### Feature, design first

The update workflow follows these three steps:

- **Update Design** Modify the design.md file directly or ask Kiro to update it in a spec session.

- **Update Requirements** After making your design or architecture changes, ask Kiro to validate and regenerate requirements to ensure they remain feasible.

- **Sync files** Navigate to the tasks.md file and choose Sync Files to reflect the changes.


# Source Control

As you work with specs, you will need to implement a source control strategy that helps you track updates and changes across both your specs and your code. The simplest way to do this is to version control your entire project workspace. This will enable you to use Git to track changes and push commits atomically for the workflow steps (you can keep task implementation as separate commits).

You should think about what version control strategy makes sense when you are working with specs. For example, do you want to create branches for each spec and then merge in later, or does a simpler workflow work?
