# Creating new applications with spec driven development

In previous labs we used the spec driven workflow to create a new application, starting with creating requirements, working through the design, and then building out the project through the implementation plan. The previous workflow started with requirements, and then generated the design after. This workflow provides you with the ability to review and change the design FIRST before the requirements are generated.

**Make sure you have your dependencies installed**

---

![Lab](/images/lab-header.png)

In this lab we are going to set our project up with everything we need.

#### Lab-01

![Lab](/images/lab-header-end.png)


1. Create a new project workspace on your machine. Create a directory called "kiro" and from within that directory, create a project workspace called "sdd-design". Use the following commands if you are using a Linux or MacOS machine, or use an equivalent command or Windows Explorer to create these directories.

Open up a new terminal, and from your home directory enter the following commands:

```
mkdir ~/kiro/sdd-design && cd sdd-design
```

and then check out the demo application into this directory and change directory to make it your project directory

```
git clone https://github.com/beechgeek/sdd-workshop-book-sharing-app
cd sdd-workshop-book-sharing-app
```
2. Now launch Kiro

```
kiro .
```

With Kiro launched we are ready to proceed.

---

![Lab](/images/lab-header.png)

In this lab we are going to add a new feature to the existing application. In previous labs we used the New Feature, Requirements workflow. In this lab we are going to look at switching to the New Feature, Design workflow.

#### Lab-02

![Lab](/images/lab-header-end.png)

1. The first thing we are going to do is to create a steering file that will help direct and influence some of the technical decisions.

From the Agent Steering panel, click on the + to create a new steering document. From the options, select project workspace steering.

Name this steering file "Python-Standards", and after pressing enter copy the following text into this new steering document in the main editor.

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

Save and exit when you have copied this into the document. You should now see that this new steering document appears with the others.

2. From the chat interface, we are going to now initiate a new spec.

From the Kiro navbar, click on the "+" next to Spec to create a new spec. In the dialog that comes up, enter the following:

"Add a new feature so that a user can export all their books in csv format. The export feature should appear in their profile page"

3. This will start the spec workflow decision process, asking you which kind of spec workflow you want to follow. Two choices will be presented: "Build a Feature" or "Fix a Bug".

Select "Build a Feature"

In the follow up dialog, you will have two options. "Requirements" or "Technical Design". Select "Technical Design" and then click on the Submit Answer.

A new dialog box will appear asking to select which design documents you want to begin with. We have added both of these, so we will leave both selected.

![design first](/images/feature-design-first.png)

After clicking on "Submit Answer" Kiro should now start the spec workflow. After a few minutes, you should see something like "I've created the high-level design document for the CSV export feature." in the chat history. We can now review the design.

4. The design.md file should open up in the main editor panel - if not, use the file explorer to open it. The design is focused on the new feature that we have asked to add, in this case exporting books in csv format.

Spend some time reviewing this. What are the differences between the design.md created with the other spec workflow?

If you want to make changes, you can now do this in one of two ways:

* interact and make changes via the chat interface
* hand edit the design.md, making sure to nudge Kiro to reload the doc once you have saved the file

5. Once you are happy to proceed, click on the "Continue" > "Generate Requirements" button at the top. This will start the requirements generation, creating the "requirements.md".

Once completed you can click on "Continue" > "Review Requirements" which nudges you to review the updated requirements doc. 

In addition to reviewing the requirements.md file, make sure you check the design.md doc. Kiro updates the design to include correctness properties for these requirements. You can use the diff icon to review these quickly.

6. The final stage of the workflow is to start the generation of the tasks via the implementation plan. From the main editor panel, click in "Continue" > "Generate Tasks" to start the generation of the plan.

After a few minutes, you should see the list of tasks needed to implement the export cvs feature.

7. Go through and complete all essential tasks and then when completed, start the application to validate that the new feature has been added successfully.

- access the application via http://127.0.0.1:5000
- register and login as a user
- test the export book feature

This is the end of this lab. You can learned how you can use this kind of spec workflow to add features to existing codebases, taking a design first approach.

![Lab](/images/lab-header-end.png)

---
