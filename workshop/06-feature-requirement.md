# Creating new applications with spec driven development

In this lab we are going to apply everything we have learned in the previous sections, and use spec driven development to build a simple web application. We are going to start fresh with a new directory and build up from the ground up to walk you through the workflow. The goal of this lab is to:

* provide a hands on overview of the spec driven workflow
* understand dependencies and ways you can interact and influence with the workflow
* look at the spec lifecycle

At the end of this lab, you will have completed both creating and updating your first spec driven project, for a new (greenfield) application. In the next lab you will apply spec driven workflows to work with an existing project (brownfield).

**Make sure you have your dependencies installed**

Before beginning, make sure you have installed the dependencies required for this workshop as outlined in the [README](/README.md).

---

![Lab](/images/lab-header.png)

In this lab we are going to set our project up with everything we need.

#### Lab-01

![Lab](/images/lab-header-end.png)


1. Create a new project workspace on your machine. Create a directory called "kiro" and from within that directory, create a project workspace called "sdd-greenfield". Use the following commands if you are using a Linux or MacOS machine, or use an equivalent command or Windows Explorer to create these directories.

Open up a new terminal, and from your home directory enter the following commands:

```
mkdir ~/kiro/sdd-greenfield && cd sdd-greenfield
```

2. Initialize git - we are going to use git to track all specification and code changes within our project - this will allow us to track and revert to a given state as we need.

```
git init
```

3. Now launch Kiro

```
kiro .
```

With Kiro launched we are ready for the next lab. Before you proceed though, spend some time navigating and exploring Kiro.

----

![Lab](/images/lab-header.png)

In this lab we are going to create a steering document that we want Kiro to use as it starts to architect and design solutions against our requirements.

#### Lab-02

![Lab](/images/lab-header-end.png)


1. From Kiro, make sure you are on the Kiro screen (click on the Kiro icon on the left hand activity bar) - the "Agent Steering" panel should be empty.

2. Click on the "+" icon, which will bring up the steering document creation menu.

![Steering document pop up menu](/images/adding-steering-menu.png)

3. Select the first option ("xxx agent steering", applies only within this project workspace) in the dialog that appears next. This will configure a project specific steering file. Enter a name for this steering file. The rule of thumb here is that it should be short but descriptive enough to help someone know what this might be. We are going to call ours "Project-Standards", so type that and then press enter.

4. This will bring up steering file in the editor. Replace the content with the following:

```
---
inclusion: always
---

# Coding Preference

You have a preference for writing code in Python. 

## Python Frameworks

When creating Python code, use the following guidance:

- Use Flask as the web framework
- Follow Flask's application factory pattern
- Use Pydantic for data validation
- Use environment variables for configuration
- Implement Flask-SQLAlchemy for database operations

## Project Structure and Layout

Use the following project structure

├ app
	├── src
	├── src/static/
	├── src/models/
	├── src/routes/
	├── src/templates/
	├── src/extensions.py

## Local and Prod configurations

- Run local development setups on 127.0.0.1:5001
- Run production configurations via gunicorn
- Configure via env variables

## Python Package Management with uv

- Use uv exclusively for Python package management in all projects.
- All Python dependencies **must be installed, synchronized, and locked** using uv
- Never use pip, pip-tools, poetry, or conda directly for dependency management
- Use these commands - Install dependencies: `uv add <package>`,  Remove dependencies: `uv remove <package>` and Sync dependencies: `uv sync`
- Run a Python script with `uv run <script-name>.py`
- Run Python tools like Pytest with `uv run pytest` or `uv run ruff`
- Launch a Python repl with `uv run python`
- Configure [tool.hatch.build.targets.wheel] packages with the correct value for the project

## Testing and PyTest

- ALWAYS fix tests that generate warning errors

## Secrets

- NEVER store Cloud provider credentials in a configuration file

```

Save the file and you should now have your steering file setup. What have we done? We have provided Kiro that when its thinking about design/code, that it needs to:

- use Python
- use specific Python frameworks
- use uv for package and dependency management

> **Where's my steering file?** You might be wondering why you cannot see your steering file in your project workspace. This is because we created a global steering file, and these reside outside of your project workspace in the **".kiro"** directory. Have a look at this directory in a separate terminal session and you will see your steering file.

5. In the Kiro IDE, click on the "+" at the top to open a new session, select Vibe. Now enter the following in the chat window. 

```
Show (don't create) me some code that implements a simple API that returns a json date object
```

Review the output - you should see that it has respected the preferences we have just defined.

---

![Lab](/images/lab-header.png)

We are going to develop a new application using the spec driven approach. The application itself is not important, but is a useful way to show the SDD workflow. We are going to create a deliberately simplified application (a web application to manage our tasks) so that we can complete a full iteration in the time of the workshop. 

#### Lab-03

1. We are going create an initial specification,so from the "Lets Build" panel, make sure that "Spec" is selected.

2. In the dialog box, enter the following

"I want to create a simple todo web application to track things I need to do"

3. After a short pause, Kiro's spec workflow decision dialog will appear asking you whether you want to "Build a Feature" or "Fix a Bug".

Notice that Kiro will recommend the most likely task - in this case, "Build a Feature".

Click on the "Submit Answer" once you have ensured that "Build a Feature" has been selected.

This will bring up the second decision dialog - whether you want to start with Requirements or with a Technical Design. As this is a greenfield application with no existing architecture or design, we are going to select Requirements (which should be the recommended option). Click on the "Submit Answer" button to continue.

Kiro will begin the spec workflow, and will create a new spec for you by generating a new "requirements.md" file. This might take 2-3 minutes, so a great time to grab your favorite drink and rehydrate!

4. Switch to the File Browser tab, and you should see a new directory called ".kiro" which now contains a new directory which will be named after your spec. What is your directory called? Within this directory you should also see the requirements.md file.

5. Switch back to the Kiro tab, and you will notice that in the top left of the Kiro widgets you will see your new spec listed. Click on this, which should reveal your requirements.md file in the main editor. You should also see that there are three boxes that contain the three steps of the workflow: requirements, design, and tasks.

6. Look at the chat interface, you should see a summary of the work that Kiro has done. Take note of the greyed out text that also shows how many Kiro credits this activity used. It will look something like:

```
Est. Credits Used: 0.39             Elapsed time: 4m 23s
```

Now that we have our requirements.md created, lets review it.

![Lab](/images/lab-header-end.png)

---

![Lab](/images/lab-header.png)

With the first artefact (requirements.md) created, we now need to review and refine. In this lab we will look at the different approaches you can take and how to then move to the next step in the workflow.

#### Lab-04

1. Open up the requirements.md and review the introduction, which expands upon the initial prompt. You will typically not need to review/edit this section, but it is worth making sure this has aligned with the feature you are trying to create.

2. Review each Requirement and User Story - do they make sense? Do they include things that you would have expected, and maybe some you did not? Are the requirements defined to the right level (i.e. not over engineered)?

3. Add a new requirement of your own. We can do this one of two ways. We can directly edit the file, or we can ask Kiro to add a new requirement via the chat interface.

Lets add a new requirement to add a help page to this application (assuming this requirement was not generated after the initial generation)

First of all try via the chat interface and enter the following:

"Can you add a new requirement that adds a help page to help users understand how to use the application"

Review the output and check the requirements.md file. It should now have a new requirement. Does it look ok?

4. You can also directly update the requirement.md if you prefer. We are not going to do that in this lab, however, if you do decide to hand edit your requirements make sure of the following:

* Before saving there is one very important check you need to make. In the earlier labs we looked at the Glossary of the requirements.md doc, which defines common terms used. Make sure that when you paste this text in, the terms match. For example "Help_Page", "Todo_Item", and "Todo_App" are all mentioned in this text.
* For changes you make, the conversation and context memory will now be out of sync so you need to nudge Kiro and remind it to reload the requirements. From the chat interface, type in the following: "I have updated the requirements - please reload and review"

5. We are now ready to proceed to the design phase. There are two ways you can do this:

* Click on the "Continue" button that appears at the top of the main editor panel. This will bring up a sub menu which asks you whether you want to create the "Design" or the "Design and Tasks". **Select "Design"**
* Type "Continue to the design phase" in the chat interface and hit return.

Kiro should start to work on the next artefact, the design.md, which we will dive into in the next lab.

> **Note!** During the generation, you might get prompted by Kiro to use one of its internal tools (web_search) as it looks to get external information about Flask best practices. You will need to click on the green triangle to accept and let Kiro run its search. You may need to do this several times.

![Lab](/images/lab-header-end.png)

---

![Lab](/images/lab-header.png)

Kiro will now use the steering documents we created initially, together with the requirements we defined in the requirements.md file to build out an initial architecture and design. In this lab we are going to dive into this.

#### Lab-05

1. In the chat interface take a look at the output of the design generation process.  It should provide some details as to what Kiro has done when creating the design.md file, before inviting you to review the design.md file.

2. If the design.md document is not already loaded into the main editor window, click on the Kiro icon on the activity bar, select your spec in the top left and this should allow you to navigate to the design document.

![Navigating to the design document](/images/kiro-design.png)

Alternatively you can switch to the file explorer, and you will see that you now have a new document in the spec directory that you explored in a previous lab. 

![opening design via file explorer](/images/kiro-design-via-explorer.png)

3. When reviewing specs, it is easier to temporary remove the chat interface. Kiro makes this easy by providing some icons in the top right of the IDE. You can see that we can toggle the chat interface by clicking on the chat icon.

![toggling chat interface](/images/kiro-window-manager.png)

Click on this to expand the editor so that its full screen.

4. Go through the design document and review the design. Check for the following:

- Did it respect the steering document we created in a previous lab?
- Did the structure look like the layout we defined in the steering doc?
- Does the data model look reasonable? Data models are an important context anchor, so it is always worth checking and double checking that the data model looks good
- Review the routes/APIs that are created - do they map to our requirements?
- Look at the design decisions - do they make sense?

We are going to quickly dive into Correctness Properties in the next lab, so keep the design document open.

![Lab](/images/lab-header-end.png)

---

![Lab](/images/lab-header.png)

One of the big challenges with using AI coding assistants is making sure that the code that we ask them to generate actually gets produced. Correctness is how Kiro helps answer this question, or more specifically, how it produces code that matches your intent.


#### Lab-06

1. Review the chat history - you should find that Kiro has output about formalizing requirements to correctness properties. What are these you might be wondering, lets dive deeper.

2. From the open design.md document, navigate down to the heading "Correctness Properties". You will notice that a number of items listed. Each correctness property that is listed validates a specific requirement. Correctness properties have not been created for everything. A property is a universal statement about how your system should behave. Kiro extracts properties from your EARS-formatted requirements (e.g. "WHEN a user types a task description and presses Enter or clicks an add button, THE Todo_System SHALL create a new Todo_Item and add it to the list", the **SHALL** is key here), and then determines which can be logically tested.

During the execution phase, Kiro will then generate hundreds or thousands of random test cases when you choose to run them. If you look further in the design.md document, you will see that Kiro defines which tools and their configuration (Hypothesis).

3. We are not going to make any changes to the design. We are going to proceed to the next step in the workflow, implementation. To do this, we can click on the "Continue" button that appears at the top in the main editor window, or type in the chat interface: "Move to implementation phase" and hit return. 

This is going to start the next step in the workflow, and Kiro is going to start creating the next artefact, the tasks.md. This might take 2-3 minutes.

![Lab](/images/lab-header-end.png)

---

![Lab](/images/lab-header.png)

In this lab we will take a look at how Kiro has taken our requirements, together with the design, and creates an implementation plan. This plan outlines all the tasks needed to create our application. Each task will be used by Kiro to generate code.

#### Lab-07

1. Review the chat interface again, and look at the summary. It is important to get into the habbit of reading these summaries to make sure that they match what you think they should have done (and more importantly, catch things they forgot to do).

2. Review the tasks.md in the main editor (use the chat icon to expand the editor like we showed in the previous lab). Review the tasks.

- Find the tasks that have been marked as optional - these are greyed out, and easily identifiable as they have an "*" before the task number
- Review the high level task activity, and the order in which they are sequenced
- Look at the linked requirements and check back to the requirements.md file to make sure they align
- Notice that above each task we have a "Start task" link - don't click on these yet.

3. From the source control icon in the activity bar, we are going to check in our changes. In the changes window enter "spec-workflow-completed" and click on the commit button. After you confirm, it should look something like this.

![committing spec to source control](/images/kiro-spec-commit-source.png)

> You might have to configure git config user.name "xx" and git config user.email "xx" if you have not already done so

Using source control to version our Kiro project allows us to revert back and maintain state between our spec and any other artifacts created. This is our baseline, the start of the project before we have created any code.

> You should use your own preferred way of managing artifacts if you have them - the above example is a simplified approach just for the purpose of this workshop

4. We are now ready to get Kiro to start generating some code from our spec. From the task.md, go to the very first task, and click on the "Start Task" icon. You should see the task.md update in the main editor change, and you should see the task change like the following:

![task started](/images/kiro-task-in-progression.png)

As you do this, pay attention to the chat interface. Whilst Kiro will be generating code, you will still be in the driving seat and Kiro will be prompting you as it asks your permission to run and execute various commands. At some point you will see a message like this appear:

![asking permission to run commands](/images/kiro-run-commands.png)

We have four options when Kiro asks us that it needs to do something:

- Edit the command -we can use the editor to make changes, which can be useful if we see that Kiro has made a mistake in the command
- Reject - we can block Kiro from running this command
- Trust command and Accept - we can add this command to Kiro's trusted commands (see more of this in the [Kiro Tools Reference section](/workshop/05-tools-and-resources.md))
- Accept command - allow Kiro to run the command

During this lab we are going to click on the "Accept command". So as it appears, click on that icon. You should now see the command run, and the output proceed in the chat interface.

5. After a short period of writing code, Kiro will announce that it has completed the task. It will typically provide a short summary of what it has done, and you will notice that in the main editor, the first task should now show as "Task Completed"

![task completed](/images/kiro-task-completed.png)

You should notice that for any completed task:

- All items under the task should show as completed, with the task box changing from [ ] to [x]
- You will see a "View Changes" link next to the Task Completed text - this will allow you to view a summarized diff of code changes made
- You will see a "View Execution" link which will take you to the start of the chat history where a given task started, allow you to review the commands that were run and the output

6. Click on the source control icon in the activity bar - you should see a list of all changes made. This will include code but also changes to your spec files.

In the message window enter "Task One" and click on Commit, answering Yes when prompted. 

You should now see Task One appear in the graph. Click back on the Kiro icon in the activity bar to get back to the Kiro screen.

7. We started the first task by clicking on the "Start task" link, but we can also do this via the chat interface. In the chat interface, type the following:

"Start the next task"

You should see Kiro begin the next task. You will follow the same process as for the first task.

- Monitor activity of what Kiro does
- When prompted, help Kiro to review and act
- Review the task summary

When finished, repeat the step and add a new commit in source control, naming the commit message after each task.

8. We can also use the chat interface to complete a number of tasks if we think there are a number of related tasks that can be executed together. We do this from the chat interface.

"Start tasks three and then four"

Review the chat interface. You should see now that it starts working on Task 3 and when complete Task 4. Once complete, add another commit (call this one Tasks three and four)

You might be wondering what happens if I click on multiple "Start Tasks" links? Kiro has a queue in which it will queue tasks as they are started. In the chat interface, you will see the following icon which will display the current task queue.

![Kiro task queue icon](/images/kiro-task-queue-icon.png)

If you click on another task before the current task has finished, it will do nothing. You will see it however in the task queue.

![view task queue](/images/kiro-task-queued.png)

9. If you want to just get Kiro to start executing through all the tasks, at the top of the main editor menu you will see an option called "Run all tasks". 

![run all tasks](/images/run-all-tasks.png)

When you click on this you have two options:

* run "all required tasks"
* run "required and optional tasks"

If you decide to take this approach, you will need to make sure that your permissions are set correctly or you may return to Kiro waiting to get permission/confirmation from you.

10. You might be wondering what happens if a task fails half way through? Maybe your laptop dies, or more likely your wifi connection gets cut off.

If this does happen, Kiro will present a message within the chat interface that there was an error. Within the implementation plan, any tasks that it was working on may change status and show something like this:

![retry](/images/retry-tasks.png)

You can click on the "Retry" link to start again, or alternatively use the chat interface and enter something like "please continue" or "task failed due to network interuption - please carry on where you left off"

11. Occasionally you might find that Kiro is "stuck" with a "Working" status in the chat interface. It does not happen frequently, but when it does I find the following helps:

* Closing terminal sessions that Kiro has opened can help nudge it
* You can prompt it to move along by entering "Are you stuck" or "You still seem stuck - do you need to try something different?" or "you still seeem stuck - this is the third reminder" to get around the issue.

> **Tip!** I also ask it why it got stuck to provide me more details so that I can use this to update my steering files.

12. Now work through the remaining tasks. Experiment with using the chat interface, the UI links. Make sure you commit changes to source control as you progress.

This will take around 10-15 minutes to complete, so feel free to grab some refreshments or stretch yours legs whilst you complete the remaining tasks.

13. The final piece is to test that the application actually runs, so from the chat interface ask "Run the application for me so I can test it in a local browser"

Review the output from the chat interface and open up a browser to test you can work with the application. Once you have confirmed this, from the chat interface, enter the following: "shut down the app, and create a README.md file for this project"

After a few minutes you should have a README.md file which should outline how to get this applicatio up and running. Review quickly before proceeding to the next lab.

![Lab](/images/lab-header-end.png)

---

![Lab](/images/lab-header.png)

It is quite common that we might need to change or add new requirements after we have completed an iteration of the spec driven development workflow. In this lab we are going to show you how this works. We are going to add a new requirement to add a Contact Us page and then work through how Kiro supports this change through the spec driven workflow.

#### Lab-08

1. Make sure any files that are open in the editor are close, and that you have stopped the application. Open up the "requirements.md" file in the main editor.

2. From the chat interface, enter the following prompt:

"Add a new requirement to this current spec add a simple Contact Us Page"

Review the output from the chat interface, and then review the requirements.md file for changes. You can review changes quickly by using the diff feature in Kiro, which will open a new tab and take you directly to any changes made and highlight the differences.

![view diff](/images/kiro-diff.png)

Review the new requirement added at the end of the requirements.md file. If this looks good, we can proceed with updating the design and adding new implementation details (tasks).

3. When you add or change requirements, this might require changes to the design document. We therefore need to make sure that we ask Kiro to review and see if any changes are required. From the chat interface, type in 

"Review and updated the design as needed to match updated requirements"

This will kick start the update workflow. After a period of time you should see a summary in the chat interface summarising any design changes made.

- Use the diff to review the changes - what changed?
- Review the Correctness properties - did they change? Were new tests added?

4. We now need to update the implementation plan to update or add new tasks to complete the changes to our requirements. We can achieve this a couple of ways in Kiro:

- use the "Sync" button within the main editor, which will kick off a process to synchronise the implementation plan and tasks to match up with the design and requirements
- use the chat interface to drive this by adding "Update implementation tasks to reflect changes in requirements and design"

![the sync button](/images/kiro-sync.png)

Keep your eyes out on the chat interface which will provide you a realtime status update of what needs to be updated. You can use the diff icon to review the new tasks once Kiro has completed. This is an example output of what you might see (your task names/number will be different, these are just mine)

```
The tasks have been updated. New tasks added:

Task 10: Implement contact page
10.1 — Create the contact route and template with email, mailing address, and support hours
10.2 — Add a Contact link to the navigation
10.3 — (Optional) Write unit tests for the contact page
Task 11: Final checkpoint — Verify all tests pass
Would you like me to execute these new tasks?
```

5. You can now start executing the new tasks, either by using the "Run all tasks" button, or by entering "Complete any outstanding tasks" in the chat interface.

After a short while, Kiro will begin working through these new tasks. Again, you might be prompted as Kiro needs to request permissions to run various commands. 

6. When Kiro has completed this new task, re-start the application and see if you now have a Contact Us page.

In this lab we walked through the workflow to make updates to an existing spec, and how we can use both the chat interface or the Kiro IDE buttons to drive and sync those changes through.

![Lab](/images/lab-header-end.png)

---

![Lab](/images/lab-header.png)

In the previous lab we made some changes to add a Contact Us page. What if we decided that this update was not what we needed and we wanted to undo this change. Whilst it might be tempting to ask Kiro to undo the change, there are more effective ways you can achieve this.

At the beginning of this lab you used Kiro's source control integration features to commit changes after tasks where completed. Using source control is one approach you can take. Kiro also provides some capabilities you should be aware of that can help you, through its revert and checkpoint features. In this next lab will explore these.

#### Lab-09

1. In the previous lab we added a new feature called Contact Us, which added new code. We might want to undo some changes, perhaps only certain files. We can use the Undo Change and Revert features from within the chat interface to undo either one or a collection of code changes.

From the chat interface, review the code that was generated by Kiro in the previous lab. After code changes, you will see the following.

![Undo code change](/images/kiro-code-undo.png)

If you click on that link, it will undo that code change. Don't do that now.

You can also revert changes done throughout the entire conversation or task. Once a task has been completed, you will see the following link above the chat interface dialog window.

![Revert code](/images/kiro-code-revert.png)

Be very careful clicking on that link as there is no confirmation or undo option! Again, we will not click on this link yet - this was just to let you see that these options allow you to control code changes and allow you to undo/revert back to a previous state.


2. Using Undo and Revert is fine grain and allows you to manage updates to your project files. Kiro provides another feature called Checkpoint. 

Each time you send a prompt to Kiro (or start a task in the implementation plan), it creates a “checkpoint”. Checkpoints appear as markers in your chat history. You can hit Restore on a checkpoint marker to rewind both your codebase and Kiro’s context back to that point in time. Any changes made to your codebase by Kiro after that checkpoint are reverted, and any context additions (chat interactions) after that point are discarded as well. 

![Checkpoint in Kiro](/images/checkpoint.png)

In the previous lab we added a new feature called Contact Us. This actually is a collection of checkpoints:

* first checkpoint was asking to add a new requirement to our spec
* second checkpoint was updating of the design document
* third checkpoint was updating the implementation plan
* fourth checkpoint was writing the code during the plan execution

Depending on what you want to do, you might want to just revert the code or you might want to revert back to the requirements updates. All you have to do is select the specific checkpoint and Kiro will revert you back to that state (updating its context in the process). Lets see how these work, starting off with reverting just the code and then the requirements.

3. From the chat interface, find the start of the conversation where you added the "Contact Us" feature (the prompt was "Add a new requirement to this current spec add a simple Contact Us Page")

After you have located it you will notice that there is some text above this. On the left you have "Checkpoint" and on the right, a link for "Restore" - it should look like this

Click on the Restore link. It should generate the following (or similar) text.

> Restoring this checkpoint discards all changes made after this point in this session and removes conversation history from context. Imports or references may break if related files changed elsewhere - you'll need to fix those manually.

It should display a list of changed or modified files that are in the scope of this change. You will be asked to confirm whether you want to "Restore Checkpoint". Click on the Confirm link, and after a few seconds you should see all those changes disappear.

Congratulations, you have now reverted back the code based cleanly to where it was before the Contact Us changes where made. Start the application and confirm that you no longer have the Contact Us page.


> As a side note. If you have just reverted the code changes, your implementation plan (tasks.md) and the code in your project workspace will now be out of sync (the tasks will be in the todo.md and marked as completed). You can address this either by manually editing the tasks file to uncheck any tasks (removing the "x" so that [x] becomes [ ]) and then saving this file. When you do this, you should notice that the task becomes active again within the implementation plan (tasks.md). The other approach is to use the "Update Tasks" link at the top of the implementation plan (tasks.md). This will then attempt to review and update the implementation plan for you, and after a few minutes Kiro will prompt you for what you want to do.
> 
> ![update tasks to refresh](/images/tasks-update.png)
> 
> I tend to edit the todo.md plan manually as this saves on tokens/credits

4. Now locate the chat window where you created the new requirement. Kiro will open new tabs for each conversation, so you will find this by looking for a tab called "Add a new requirement".

![revert whole requirement](/images/kiro-checkpoint-requirement.png)

Click on the Restore link, and then confirm when you see the Restore Checkpoint pop up appear above the chat interface dialog box. The current chat conversation will disappear once you have done this and you should now be back at where you started.

5. In the previous examples you used Kiro native features to help you navigate state within your project. You can also use source control. During the earlier labs you initialized git and committed code as tasks were completed.

We are not going to explore this in this workshop, but experiment and see which approach works best for you.


![Lab](/images/lab-header-end.png)

---

![Lab](/images/lab-header.png)

You can create many specs for a given application. In this next lab we are going to create a completely new spec, building on from the code that Kiro has already generated for us. We are going to add a new feature to export our todo's in csv format.

#### Lab-10

1. Ensure the application is stopped, and that all open files are closed in the editor. Switch to the Kiro tab using the Kiro icon in the activity bar.

2. Located the Specs section in the top left, which should already have the first spec we created (todo-web-app or something similar). Click on the "+" on the right hand side.

3. From the dialog that pops up, enter the following text:

"Create a new spec that add a new capability to allow me to export my todos as a csv file"

Review the output in the chat interface. You will be asked to go through the spec workflow decision tree. Use the same settings as before (Build a Feature, Requirements).

Kiro will review existing specs you have created. In our case, it is going to create a new spec. However, if Kiro thinks that what you are asking for might be better as a new requirement to an existing spec, it will inform you and start that process (which we have done in previous labs)

4. After a few moments, we should now see a new requirements.md appear in the main editor. If you look at the left hand side in the Spec section, you will also see that we have a new spec listed (csv-export or something similar). If you switch to the file explorer, you will see that under the .kiro directory, under specs you now have a new directory that has been created for this new spec.

5. Switch back to the Kiro view, and now work through the three steps of the workflow to complete this new spec. This will take around 5-10 minutes. As you do this, look for the following:

- notice how Kiro checks the existing application functionality during the three phases of the workflow
- apply what you learned for the first spec as you work through the three phases: requirements, design, and implementation
- as you start running tasks during the implementation plan, make sure you watch out and respond to prompts when Kiro needs permissions to run commands 

6. Once Kiro has completed all the tasks, start the application and test out this new feature to make sure it works.


![Lab](/images/lab-header-end.png)

---

### Lab Completed

Congratulations, you have now completed the first set of labs and are now ready to explore the world of spec driven development. Before you go, if you are hungry for more, then take a look at some of these suggested next steps to give you

**Recommended next steps**

* To dive deeper, run through the labs again this time selecting to run all tasks during the implementation phase. This will take longer, and use more Kiro credits. You will get to see how Kiro generates and then runs property based testing.
* Add new requirements to an existing spec - Kiro will make an attempt to put a new requirement in either an existing spec or create a new one. Try adding a new feature that allows you to add comments or updates to a task to an existing spec (open the spec up and use the chat to add this as a new requirement)
* Go through and add additional specs to this project - perhaps add simple authentication using email addresses, or maybe add persistence to a database
* Dive deeper into steering documents and how these influence the output Kiro generates

Click on [Existing Codebases](/workshop/04-brownfield.md) to proceed to the next section where we show how you can use SDD with existing code you have

