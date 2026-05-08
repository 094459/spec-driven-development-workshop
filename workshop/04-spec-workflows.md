In this section we will dive a little deeper into the different spec workflows that you will typically use on a day to day basis.

The workflow you choose follows a logical progression between three phases with decision points, ensuring each step is properly completed before moving to the next. We have seen the artefacts that these phases produce already (the requirements.md, the design.md, and the tasks.md).

The workflow is initiated when we create a new spec via a prompt in the chat interface. Within the chat interface you are guided through a series of question as to which workflow you want to follow:

![spec workflows](/images/Pasted%20image%2020260507145810.png)

Kiro will transform that prompt and creates the initial spec. Kiro creates a new directory which is used as a container for all the artefacts produced (.kiro/{specname}).

## Starting Point

There are three different spec workflows that you will typically follow:

* Building a Feature, Requirements First
* Building a Feature, Design First
* Fixing Bugs

Feature Specs provide a structured approach to building new features, guiding you through requirements gathering, technical design, and implementation planning. The Bugfix Spec models how experienced developers approach bug fixes, and provide a structured approach using that workflow, guiding you through root cause analysis, fix design, and regression prevention to ensure surgical, reliable fixes.

The rest of the lab we will dive into these in more detail.

## Feature Specs - Requirements First

The Requirements-First workflow is the traditional approach to Feature Specs, starting with what the system should do before determining how to build it.

### When to use

This workflow is ideal when:

- **Clear user stories** - You have well-defined behavior that Kiro can use to create user stories
- **Flexible architecture** - Technical design can be adapted to meet requirements
- **Greenfield projects** - Starting fresh without existing technical constraints

### Workflow

Before starting, you should ensure that you have configured any supporting context that you might need - see the context engineering lab.

The workflow is initiated by selecting Spec and then entering either the initial intent via the chat interface or the Kiro sidebar. Within the chat interface, you will be asked questions and guided through the decision making process.

![workflow](/images/Pasted%20image%2020260507213005.png)

Under the covers Kiro will create a new directory in the project workspace called ".kiro/specs" and within this a new directory will be created that is the holding place for specs. Within this ".kiro/specs" directory, a directory will be created for this specific spec. This directory will be where all artefacts are created (requirements.md, design.md, and tasks.md)

The workflow starts with creating the requirements, followed by the design, and then the implementation plan.

**Phase 1: Requirements** 

- Purpose: Transform vague feature ideas into clear, testable requirements
- Key Activities: Capture user stories that express value and purpose, define acceptance criteria using EARS (Easy Approach to Requirements Syntax), identify edge cases and constraints, and validate completeness and feasibility
- Benefits: Ensures all stakeholders understand what's being built, provides clear success criteria for implementation, reduces scope creep and feature drift, and creates a foundation for testing and validation

**Phase 2: Design**

- Purpose: Create a comprehensive technical plan for implementation
- Key Activities:Research technical approaches and constraints, define system architecture and component interactions, specify data models and interfaces, plan error handling and testing strategies
- Benefits: Identifies technical challenges before coding begins, enables better estimation and resource planning, and provides a roadmap for implementation, documents design decisions and their rationale

**Phase 3: Tasks**

- Purpose: Break down the design into actionable, sequential implementation steps
- Key Activities: Convert design elements into specific coding tasks, sequence tasks to enable incremental progress, define clear objectives and completion criteria, reference requirements to ensure traceability
- Benefits: Makes large features manageable through decomposition, enables parallel work and better progress tracking, reduces cognitive load during implementation, facilitates code review and quality assurance

## Feature Specs - Design First

The Design-First workflow starts with a technical design or system architecture and derives feasible requirements from it. Kiro will let you select which design documents you want to incorporate into the design.md, and you have the choice of two

* High Level Design - Full architecture including system architecture diagram, component descriptions and interactions, technical approach and patterns, and non-functional properties (performance, scalability, security). 
* Low Level Design - Focused on implementation details, such as algorithmic pseudocode, interface definitions and contracts, key data structures, and non-functional properties

Depending on which you select, the spec creation process will map your intent into the design.md. The design.md will look different to the other spec workflow.

### When to use

This workflow is ideal when:

- **Rapid prototyping** - You know the tech stack and want to explore what's possible
- **Technical constraints** - System must meet strict non-functional requirements (latency, throughput, uptime, compliance)
- **Existing designs** - You have architecture diagrams or design documents to port into Kiro
- **Feasibility exploration** - You want to understand what requirements are achievable given a design
- **Strong opinions** - You have specific architectural preferences or constraints

### Workflow

The workflow is similar to the Requirements First, but there are a few important differences.

* As with the requirements first workflow, you should ensure that you have configured any supporting context that you might need - see the context engineering lab.

The workflow is initiated by selecting Spec and then entering either the initial intent via the chat interface or the Kiro sidebar. 

![workflow](/images/Pasted%20image%2020260507214053.png)

Under the covers Kiro will create a new directory in the project workspace called ".kiro/specs" and within this a new directory will be created that is the holding place for specs. Within this ".kiro/specs" directory, a directory will be created for this specific spec. This directory will be where all artefacts are created (requirements.md, design.md, and tasks.md)

The workflow starts with creating the design.md first, which is then followed by the requirements.md, and then the implementation plan.

**Phase 1: Design**

- Purpose: Create a comprehensive technical plan for implementation
- Key Activities: Generates a design that meets the provided design documentation (high level, low level, or both) with the intent. It is important to note that at this stage some of the design will not be there -for example, correctness properties, as these need to have well formed (EARS) requirements to work from
- Benefits:  Identifies technical challenges before coding begins, enables better estimation and resource planning, and provides a roadmap for implementation, documents design decisions and their rationale

**Phase 2:  Requirements** 

- Purpose: Transform vague feature ideas into clear, testable requirements
- Key Activities: Capture user stories that express value and purpose, define acceptance criteria using EARS (Easy Approach to Requirements Syntax), identify edge cases and constraints, and validate completeness and feasibility
- Benefits: Ensures all stakeholders understand what's being built, provides clear success criteria for implementation, reduces scope creep and feature drift, and creates a foundation for testing and validation

**Phase 3: Tasks**

- Purpose: Break down the design into actionable, sequential implementation steps
- Key Activities: Convert design elements into specific coding tasks, sequence tasks to enable incremental progress, define clear objectives and completion criteria, reference requirements to ensure traceability
- Benefits: Makes large features manageable through decomposition, enables parallel work and better progress tracking, reduces cognitive load during implementation, facilitates code review and quality assurance


## BugFix Specs

The Bugfix Spec workflow guides you through root cause analysis, fix design, and regression prevention to ensure surgical, reliable fixes.

### When to use

Use this workflow when:

- Complex bugs requiring root cause analysis
- Bugs in critical code paths where regressions are costly
- Bugs that need documentation for compliance or team knowledge
- Situations where previous fix attempts caused regressions

### Workflow

This is a very different workflow to the previous workflows. From the chat interface, you ask that you want to create a bugfix spec, and provide details (high level). For example:

```
When running the application code base (book sharing app). Logged in as a user, attempting to return a book doesn't clear the current borrower — ghost borrower. I can reproduce this as follows:

1. User A lists a book
2. User B requests to borrow it, User A approves
3. User B returns the book
4. Go to User B's "Currently Borrowed" page 
```

Kiro will attempt to understand and recommend a bugfix spec, which you can select from the menu that appears in the chat interface.

![workflow](/images/Pasted%20image%2020260507221131.png)

This will then kick off the creation of the bugfix workflow. This still has three phases in its workflow, but starts with the bugfix.md, where you define the defect that needs to be resolved, and then the design.md and tasks.md where those fixes will flow through the same workflow steps as with the other spec workflows.

The bugfix.md has a number of sections:

* Current behaviour (defect)
* Expected behaviour (correct function)
* Unchanged behaviour (regression prevention)

![bugfix-workflow](/images/Pasted%20image%2020260507221835.png)

The design.md produced is not the same as with the other spec workflows. The design.md is focused on just design changes, tests, correctness properties and any other supporting changes needed to support the fix.

The tasks.md follows the same format - the key difference here is that the tasks will be scoped on how to implement the fix that has been identified within the design. Whereas in the other spec workflows these are marked as optional by default, with bugfix spec they are required.

**Phase 1: Bugfix - Analysis**

* Purpose: The Bugfix Spec models how experienced developers approach bug fixes
- Key Activities: Provide a structured approach to guide you through root cause analysis, fix design, and regression prevention to ensure surgical, reliable fixes.
- Benefits: Explicit constraints ensure only necessary changes are made. It reduces regressions as unchanged behaviour is documented and tested. Fixes are documented, with a complete record of the bug, fix, and reasoning for future reference. 

**Phase 2: Design**

* Purpose: The Kiro explores the codebase to root cause the issue and generates a `design.md`
- Key Activities: Root cause analysis, propose fix, and look for properties to test for to validate fix and ensure no regressions

**Phase 3: Tasks**

* Purpose: Implementation tasks are generated with [property-based tests (PBTs)](https://kiro.dev/docs/specs/correctness) that validate the bug is reproducible, fixed, and does not introduce regressions
- Key Activities: Reproduce bug, fix bug, test for regressions