
## What is a "spec"?

With all this talk of "specification" you are probably thinking, what exactly is a "spec"?

Specs bridge the gap between conceptual product requirements and technical implementation details, ensuring alignment and reducing development iterations.  A spec is a collection of resources that are used to implement a feature, or tackle an issue/defect.

Specs have a number of characteristics:

- they are structured, written documents (in markdown)
- the structure is optimised for specific activities
- they are organised together as a collection

Specs follow a three-part workflow that takes you from intent to implementation. The workflow produces a number of written documents: **requirements.md** (the requirements, or intent), **design.md** (the technical design), and **tasks.md** (the implementation tasks needed to achieve the requirements with the defined design).

Kiro offers a set of distinctive and opinionated spec workflows you can follow. 

* **New Feature spec workflow (Requirements First)** - this workflow starts with a well defined requirements document which you can iterate on, before proceeding with the design and implementation phases. This workflow is great when you have well-defined behavior that Kiro can use to create user stories, the technical design can be adapted to meet the requirements, and/or have few technical constraints (Greenfield development)

- **New Feature spec workflow (Design First)** - this workflow starts with a technical design or system architecture and derives feasible requirements from it. It works great in a number of use cases such as where you know the tech stack and want to explore what's possible, or the system must meet strict non-functional requirements (latency, throughput, uptime, compliance). It is also a good choice where you have very strong opinionated/specific architecture preferences you need to maintain, or want to explore feasibility of what is achievable given that design. It is a solid choice for Brownfield applications

> It is important to know which workflow you want to use as you cannot change these later.

You might be wondering how do you know which one to use? You will gain an intuition for this over time, but the following is a good starting point:

**Choose Requirements First when:**

- You know the behaviour of the system you want to build
- Architecture is flexible and can be designed to meet needs
- Building product features driven by customer feedback
- Starting without technical constraints

**Choose Design First when:**

- You have an existing technical design or architecture
- System must meet strict non-functional requirements (latency, throughput, compliance)
- Prototyping with a specific tech stack
- Exploring technical feasibility before committing to scope

|                 | Requirements                              | Design                                            |
| --------------- | ----------------------------------------- | ------------------------------------------------- |
| **Start with**  | System behavior, captured as requirements | Technical design, architecture or pseudocode      |
| **Generate**    | Design from requirements                  | Requirements from design                          |
| **Best for**    | Product-driven development                | Technically-constrained or design-driven projects |
| **Ensures**     | Desired behavior is specified             | Technical feasibility                             |
| **Flexibility** | Implementation can adapt                  | Requirements can adapt                            |

We will explore these in more detail later on in this lab.

**Other kinds of workflows**

In addition to the spec workflows for feature development, Kiro also supports emerging new kinds of spec workflows.

* **BugFix workflow** - this workflow provides a structured approach that guides you through root cause analysis, fix design, and regression prevention to ensure surgical, reliable fixes. This use case is less about features and more about stability.

This workflow produces its own artefact - the **bugfix.md** file, which we will look at later.

## Spec Artefacts

Following a spec workflow leads to creating a number of artefacts, which we will explore in this lab.
### Requirements

When working with Spec workflows for new features, one of the key artefacts generated are requirements documents. The **"requirements.md"**, has a consistent structure

* An introduction that outlines what the outcome (intent) of this requirement is - this is where Kiro has translated your initial prompt into a more detailed overview of what this requirement will deliver
* A glossary provides a set of terms and definitions that provide consistency in the defined requirements
* Requirements themselves, that are defined using EARS (Easy Approach to Requirements Syntax) notation to provide structured, testable requirements.

Here is an example of a requirements document that shows each of the three parts of the requirements doc. The intent (orange), the glossary (pink), and the requirements (blue).

![requirements-doc](/images/Pasted%20image%2020260507144919.png)

#### Easy Approach to Requirements Syntax (EARS)

The bulk of the **requirements.md** file are instructions defined in EARS format. They follow an easy to understand and straight forward format using a recurring pattern:

* Define the requirement with a user story
* Define acceptance criteria

##### Defining the user story

Each requirement that is created has an associated user story that outlines what this requirement will deliver. It will have a title and a sequence number.

These will be referenced in subsequent artefacts that are created to help build lineage between the requirement (and user story), and design and implementation details (design decisions and actual code generated)

##### Defining acceptance criteria

Each requirement will define the acceptance criteria using the following syntax:

```
WHEN [condition/event]
THE [system] SHALL [expected behaviour]
```

SYSTEM will be replaced by a term from the glossary to ensure that the requirement refers to the correct item.

#### Refining your requirements

The first version of the **requirements.md** file is rarely 100%, and so you will need to iterate on this. Consider the following as you do this:

- **Over-engineered requirements** - Check for over engineered requirements and edit ruthlessly based on what you actually need
- **Review with Stakeholders** - Get feedback on completeness and accuracy from users and other stakeholders
- **Identify Gaps** - Look for missing scenarios or unclear requirements
- **Clarify Ambiguities** - Resolve any vague or conflicting requirements
- **Add Missing Details** - Include edge cases and error handling

**Common Pitfalls**

There are some common pitfalls that you might fall into when you first start off, so check this list and adjust your requirements as needed.

- **Vague Requirements** - Problem: "System should be fast" Solution: "WHEN user requests data THEN system SHALL respond within 2 seconds"
- **Implementation Details in Requirements** - Problem: "System shall use Redis for caching" Solution: "WHEN user requests frequently accessed data THEN system SHALL return cached results"
- **Missing Error Cases** - Problem: Only defining happy path scenarios Solution: Always include WHEN/IF statements for error conditions
- **Conflicting Requirements** - Problem: Requirements that contradict each other Solution: Review all requirements together and resolve conflicts explicitly
- **Untestable Requirements** - Problem: "System should be user-friendly" Solution: "WHEN new user completes onboarding THEN system SHALL require no more than 3 clicks to reach main features"

#### Getting requirements from external systems

If your requirements or designs already exist in another system (such as Linear, JIRA, Confluence, or Word documents), you have options:

* Using MCP integration -  If your requirements tool has an MCP Server you can connect it to directly import requirements into your spec session. 

* Manual import - you can copy your existing requirements (e.g. `foo-prfaq.md`) into a new file in your repo and open a spec chat session and say `#foo-prfaq.md Generate a spec from it`. Kiro will read your requirements, and generate requirement and design specs.

It is outside the scope of this workshop to do this, but this is a common question asked so including this for completeness.

#### Updating your requirements

You can update the **requirements.md** file in two ways. You can use the Kiro editor to make changes, or you can ask Kiro to make those changes via the chat interface.

In practice (and as you being to work with specs on a more frequent basis) you are likely to use both. As good as Kiro is at taking your prompts and making changes, sometimes it is just quicker to edit requirements.md by hand, or provide a level of detail that only hand editing will provide.

It is worth re-iterating that when you make any changes to the specification documents through edits in the editor, you will need to remind Kiro to reload them. We need to do this because when Kiro generated the initial requirements.md, it is still in its short term memory (context window). A prompt such as:

```
Please reload the requirements.md as I have made changes
```

Kiro will provide you a positive confirmation of the changes made, so make sure you look out for that and confirm that it is what you have done.

### Design

The **design.md** provides the technical design that your spec is anchored in. The document (written in markdown) follows a specific structure, and includes the following sections:

- **Key design decisions**
- **Architecture**
- **Components and Interfaces**
- **Data Models**
- **Error Handling**
- **Test Strategy**
- **Security Considerations**
- **Performance Optimizations**
- **Correctness Properties**

Here is an example of a requirements **design.md** document

![design document](/images/Screenshot%202026-05-07%20at%2016.40.34.png)

#### Reviewing the design

It is important to spend time reviewing and editing the design.md file. When reviewing the design.md make sure that you:

- **Include examples** - throughout the document you should see relevant examples that will help steer the AI coding agent when generating code
- **Edit ruthlessly** - as these are generated by an LLM, design documents can be longer and more verbose than they need to. They often over-engineer, so look out for this and edit as needed based on your use case
- **Missing items** - check and find out what is missing - missing components or missing details are frequent things that you will catch during the review
- **Alignment** - review to make sure design choices make sense (context)
- **Clarity** - ensure that technology choices are clear - do these line up with what you expect? do they match your steering documents?

You should also consider the use case you have - if you are doing a simple PoC, then maybe you can edit the design down and remove some of the sections. This will simplify the next step in the workflow, which uses a combination of the requirements and design to break down the development task into more discrete tasks.

#### Influencing your design

You might be wondering how do I influence the creation of the design document. If you have started with the design first workflow, then you are already starting with a design document or architecture and Kiro will use that to build its design document.

If you are using the requirements first workflow, then you can influence the design by using something in Kiro called Steering Documents. These are context files in markdown, or Agent Skills that you might have created, or even MCP Servers that you use to integrate with your internal systems.

When you configure steering documents, these are used to influence both the design, but also the output of code generated during the implementation phase (we are coming to that next).

Steering documents will be covered in the next section in detail, so hold onto your hat for the moment.

#### Updating your design

As with the requirements.md, you can update or make changes to your design document through the chat interface or by hand editing.

If you hand edit, then make sure to prompt in the chat interface to update the current context window session that Kiro has. I use a prompt like the following:

"I have updated the design.md please review and reload"

It should provide you a summary of the key changes you have made.

#### Chicken or Egg

We have so far looked at the design.md and the requirements.md, but which one you start with depends on the spec workflow you have chosen.

* Requirements First -  when a spec is created using this spec workflow, the requirements.md will be created first, and the design will follow
* Design First - when you choose this spec workflow, Kiro will generate the design.md first before generating the requirements

You can see which kind of spec workflow you are working with, as the order of the requirements and design will be different as you can see from the following example screenshots.

![spec workflows](/images/Pasted%20image%2020260507163626.png)

### Implementation Plan

The final artefact that is produced as part of a spec is the implementation plan, which creates a markdown file called "tasks.md". The implementation plan tasks your intent and your design, and creates a series of tasks that will be used to create the feature.

This document contains a standard structured that defines:

* An overview section that provides an outline of the plan
* High level task groupings that group together a series of related tasks
* The tasks themselves, each with a sequence reference
* A reference back to the source requirements in the requirements.md
* A Notes section at the end of the document

Whilst tasks.md is a markdown document, within the Kiro IDE, each task contains a UI widget that allows you to interact with tasks and task groups - you will see this when we get hands on in later labs.

This is what a sample tasks.md look like.

![implementation plan](/images/Pasted%20image%2020260507174217.png)

#### Reviewing Tasks

When reviewing your tasks.md file, there are two dimensions you need to think about: the tasks themselves, and the order in which tasks are ordered within the tasks.md

This is the mental model I follow, from the point of view of an agent having the info it needs to generate code:

- **Clear Objective** - What specific code needs to be written or modified as part of this task
- **Implementation Details** - Specific files, components, or functions to create, and how these match requirements/design
- **Requirements Traceability** - All tasks should reference specific requirements being implemented
- **Testing Expectations** - Depending on what you have asked, make sure that the appropriate level of tests that should be written or updated are included

#### Optimising Task Sequence

Task sequence refers to how the tasks are grouped together to form a cohesive execution plan. Kiro will structure tasks in a logical sequence, and normally these are good enough to use. However it is worth diving deeper into this so that you can understand and potentially change how these tasks are completed.

There are a number of different strategies you can take when structuring your tasks. These include:

- **Core First** - Build essential functionality before optional features
- **Risk First** - Tackle uncertain or complex tasks early
- **Value First** - Implement high value features that can be tested quickly

**Core First**

The sequence of tasks will typically look like:

1. Project setup and core interfaces
2. Data models and validation
3. Data access layer
4. Business logic services
5. API endpoints
6. Integration and wiring

- Advantages - Establishes solid foundation before building features, reduces rework from architectural changes, clear dependency chain
- Disadvantages - Longer time before visible functionality, risk of over-engineering foundation

**Risk First**

The sequence of tasks will typically look like:

1. Most uncertain/complex components
2. External integrations and dependencies
3. Core business logic
4. User interface and experience
5. Polish and optimization

- Advantages - Early validation of technical feasibility, reduces project risk, informs architectural decisions
- Disadvantages -may not deliver user value early, requires strong technical expertise

**Value First**

The sequence of tasks will typically look like:

1. Core user registration (end-to-end)
2. User authentication (end-to-end)
3. User profile management (end-to-end)
4. Advanced features and optimizations

- Advantages - Early user value delivery, faster feedback cycles, and reduced integration risk
- Disadvantages - May require refactoring as features expand, and potential for technical debt

**Hybrid**

There is another approach, which may be suitable for many as a starting point. The Hybrid approach balances out features from the previous.

The sequence of tasks will typically look like:

1. Minimal foundation (core interfaces, basic setup)
2. High-risk/high-value feature slice
3. Expand foundation as needed
4. Additional feature slices
5. Integration and polish

- Advantages - Balances risk management with early value, flexible and adaptable, and pragmatic approach

Throughout the rest of this workshop we are going to stick with the default sequence that Kiro generates. You should however consider these alternative sequence approaches based on the use case you are working on as they may give you a better outcome.

#### Managing Task dependencies

One thing you need to think about as you review and potentially update the tasks is how your tasks related to each other, specifically which tasks depend on others and whether some tasks need to be completed before others can be started.

You can group Task dependency in three categories:

- **Technical** - Code components that must exist before others can be built. For example, Database models before services that use them, Authentication middleware before protected endpoints, or Configuration setup before feature implementation
- **Logical** - Features that build conceptually on others. For example, User profile editing requires user registration, Password reset requires user authentication,Advanced search requires basic search
- **Data** - Tasks that require specific data or state to exist. For example, User dashboard requires user data, Reporting features require transaction data, or Admin features require user roles

**Circular Dependencies**

In some situations you might encounter a situation where you have a circular dependency. For example, you might have a User service that depends on an Auth service, but that Auth service itself depends on the User service. Three strategies that can help:

**Interface extraction**

```
- [ ] 1.1 Create IUserService and IAuthService interfaces
- [ ] 1.2 Implement UserService using IAuthService interface
- [ ] 1.3 Implement AuthService using IUserService interface
- [ ] 1.4 Wire up dependency injection

```

**Layered approach**

```
- [ ] 1.1 Create User data model and basic CRUD
- [ ] 1.2 Create Auth service using User CRUD
- [ ] 1.3 Enhance User service with Auth integration

```

**Decoupling**

```
- [ ] 1.1 Create event system for user/auth communication
- [ ] 1.2 Implement User service with event publishing
- [ ] 1.3 Implement Auth service with event listening

```

### Testing and Correctness

#### Testing

The implementation plan outlines how Kiro will break down the feature into a set of steps (task) which are used to generate code. As part of this, Kiro will create corresponding tasks that cover the generation of tests.

![testing](/images/Screenshot%202026-05-07%20at%2017.01.28.png)

Kiro will mark these tasks as optional, which means you will need to enable these tasks if you want tests to be generated. This provides you with the flexibility of whether you want to go faster (and keep testing tasks disabled), or need more confidence in the code.

You can click on "Make task required" to let Kiro write the tests. You can also do this by editing the tasks.md file, removing the " * "  by the task id. The " * " is how you can mark any task as "optional".

#### Correctness

When AI generates code, how do you know it matches your intent? This is where something called Property Based Testing (PBT) can be very helpful. 

PBT is a step towards a fundamental shift in how we think about correctness with AI, moving from checking individual examples to validating universal properties across entire input spaces. Traditional unit tests only check specific examples, and whoever writes them—human or AI—is limited by their own biases. By automatically translating natural language specifications into executable properties and generating comprehensive test cases, Kiro creates a powerful feedback loop that helps both AI agents and human developers build more reliable software. This approach not only finds bugs that traditional testing misses, but also maintains a clear, traceable link between your requirements and the tests that validate them.

While PBT cannot guarantee the absence of all bugs, it provides significantly stronger evidence of correctness than example-based testing alone, making it an essential tool for specification-driven development.

A property is a universal statement about how your system should behave. Properties express the invariants and contracts that should always be true in your system, regardless of the specific data involved. This maps well to the EARS syntax for defining requirements, allowing correctness properties to be extracted where we see terms such as SHALL or ALWAYS.

When the design.md document is generated, there is a section that outlines identified correctness properties. For example, when I look at my design.md document,  I see the following correctness property defined.

```
### Property 1: Valid registration creates a retrievable user

*For any* valid registration input (username, email with valid format, password ≥ 8 characters), calling register and then looking up the user by email should return a user with matching username and email.  

**Validates: Requirements 1.1**
```

It maps to a requirement from the requirements.md document

```
1. WHEN a valid registration request containing username, email, and password is received, THE Auth_Server SHALL create a new user account and return a success confirmation

2. WHEN a registration request contains an email already associated with an existing account, THE Auth_Server SHALL reject the request with a descriptive conflict error

3. WHEN a registration request contains a password shorter than 8 characters, THE Auth_Server SHALL reject the request with a validation error describing the minimum length requirement

4. THE Auth_Server SHALL store passwords using a one-way cryptographic hash with a unique salt per user
```

And a corresponding implementation task is created (Property 1 below)

![testing tasks](/images/Screenshot%202026-05-07%20at%2017.00.37.png)

This is a very powerful feature of Kiro that providers stronger confidence in the generated code.

### Managing specs across your team

Specs are designed to be version-controlled, making them easily shareable across your team. Store specs directly in your project repository alongside the code they describe. This keeps all project artefacts together and maintains the connection between requirements and implementation.

The current guidance from the Kiro team if you want to automate/simplify this is to:

1. **Create a central specs repository** - Establish a dedicated repository for shared specifications that multiple projects can reference.
2. **Use Git submodules or package references** - Link your central specs to individual projects using Git submodules, package references, or symbolic links depending on your development environment.
3. **Implement cross-repository workflows** - Develop processes for proposing, reviewing, and updating shared specs that affect multiple projects.

You can expect improvements in this area as this is frequently the most asked area for improvement.

**Specs and Kiro session data**

One thing to be aware of is that whilst the artefacts created (markdown files and supporting resources) can be managed in your project repo, the session data of how you created these in Kiro will only work for the machine that these were created on. 

For example, you can click on your implementation plan, and look at the history of a task and it will bring you back that session in your chat interface. This will only work on the machine that it was created on as this information is Kiro session data.