# The evolution that led to specification driven development

In this short section we will take a look at how AI coding assistants have been evolving over the past few years, leading to the next generation of tools that are supporting spec driven development (SDD). It will explore the problems that spec driven development is solving, and also address some common questions that I hear come up as developers wrap their heads around this new approach.

## Evolution of AI Coding Assistants

![evolution timeline](/images/Pasted%20image%2020260507115023.png)

Over the past 2-3 years, we have seen AI Coding Assistants rapidly innovate and take advantage of improvements in large language models. From simple tab completion and code blocks, to writing larger pieces of code, and then onto the more recent agentic workflows where they are able to iterate and complete entire code bases.

Developers using these tools have identified a number of use cases where this approach shines: experimentation and rapid prototyping, one shot automation, and helping them to learning. We saw the emergence of "Vibe Coding" to describe how developers would let "AI off its leash" to create code with little oversight and control.

> **Characteristics of Vibe Coding**
>
> * Rapid and conversational - CHat Orientated Programming (CHOP)
> * Iterative, back and forth
> * Ephemeral in nature, once your session was over, it was gone
> * Point in time prompts that you needed to manage
> * Context was transient and point in time

Many saw the potential, but had questions or concerns: these approaches worked for small scale tasks but tended to struggle working with larger codebases and could not scale, the lack of control and reproducibility was a concern, and there were fears of quality of the generated code. This led to a whole new category of job description - Vibe Coding Cleanup Specialist!

---

## Emergence of good practices

Developers quickly found out and shared good practices, and were able to make AI coding assistants work more effectively. The three key areas of these were around breaking down problems into smaller tasks, being more precise and accurate in what you are asking, and the importance of context.

* Breaking down large problems - developers quickly learned that AI coding assistants worked more effectively when tackling discrete tasks, and that the key was to take a problem and decompose this into the right chunks to work with.

* Specificity and Clarity - prompt engineering became a thing, and developers quickly took this and developed good practices around how to craft prompts for software engineering tasks - the level of detail required, the use of examples, meta prompting, and the importance of iterating and refining your prompt

* Context, context, context - was probably the most important part that developers discovered affected the quality of the outputs of AI coding assistants, and so was born context engineering

Developers began to share their experiences and best practices. Calm coding, the art of taking a step back and being more intentional was a common pattern that emerged. This pattern helped shape better context and prompts, and produce more focused output.Developers began to produce tools to help simplify these learnings - whether it was tools to break down problems into smaller tasks, or opinionated tools that guided you through specific workflows. 

---

## Spec driven development emerges

> "You don’t program by chatting. You program by writing documents"

Blog posts like [Chat is a bad UI pattern for development tools](https://danieldelaney.net/chat/) began to share thinking that the current CHOP approach needed to change, and started to explore what a more focused, intentional approach would look like.

Developers were talking, practitioners were sharing tools and prototypes, and key elements began to emerge:

* **Clarity Before Code** - Clarity of thought and purpose must precede implementation. By investing time in understanding requirements, designing solutions, and planning implementation, we reduce uncertainty, minimise rework, and increase the likelihood of building the right thing correctly.

* **Iterative Refinement** - Design for iterative improvement. Rather than moving linearly from idea to implementation, the methodology encourages refinement and validation at each step. This approach catches issues early when they're less expensive to fix and ensures that each phase builds solidly on the previous one.

* **Documentation as Communication** - move away from ephemeral prompts to tools that help you communicate and align stakeholders, preserve decision rationale, and provide context for future maintenance and enhancement. 

Spec driven development is an approach that helps developers start with intent, and then move through collecting the right supporting context to generate technical designs and implementation details. It breaks down the implementation into discrete tasks that AI coding assistants can execute, supporting by just the right level of context.

**Characteristics of Spec driven development**

Spec driven development brings together the good practices that have been emerging. It puts a  focus on upfront planning and intent. It looks at how to break down work into discrete tasks, whether that is new or existing work. It bakes in good context engineering practices as first class artefacts, using the idea of **Steering documents** that ground agentic outputs. And it helps create lineage between intent and code, that allows developers to have a stronger relationship and ownership of the code generated.

---

## Use Cases

Spec driven development is still pretty new, and developers are still exploring where it provides a good fit over existing approaches. The use cases are still emerging, and this is a fast moving space. You might not need or want to apply spec driven development for every activity you do, so consider this a list that will help you assess your use case.

### Strong candidates

* Complex Features: When building features with multiple components, integrations, or user interactions where you have clear requirements
* Resolving defects: Ensuring that defects are fixed using a structured approach
* High-Stakes Projects: When the cost of failure or rework is significant
* Team Collaboration: When multiple developers or stakeholders need to coordinate
* Knowledge Transfer: When documentation and knowledge preservation are important
* AI-Assisted Development: When working with AI tools that benefit from clear, structured input
* Regulatory/compliance: Where you need strong lineage and audit trails between requirements and features (specs = audit trails)
 

### Less Suitable Scenarios

Whilst you can still use spec driven development for these use cases, your mileage will vary. For example, Vibe Coding is a great way to generate high fidelity prototypes to get early feedback from your stakeholders. Using Vibe mode may be more effective for that use case. Also this list is nuanced - for example, in the context of a spec driven development session, simple bug fixes as well as the use of established patterns is complimentary. 

* Simple Bug Fixes: When the change is straightforward and well-understood (overhead exceeds value)
* Experimental Prototypes: When the goal is rapid experimentation rather than production code (you lack the clarity specs require)
* Time critical Hotfixes: When immediate action is required without time for planning
* Well established Patterns: When implementing standard, repetitive functionality

## Vibe vs Spec

You might be thinking that spec driven development means we can leave vibe coding behind. The reality is that Vibe coding can still provide a lot of value, and can be super useful when combined with spec driven development.

You can use Vibe coding to explore a domain, allowing you to quickly immerse yourself in the problem you are looking to solve. Vibe coding will expose gaps in knowledge which you can address through your AI tools.  It will allow you to start presenting details that you might have overlooked. If you are new to the domain, you can use Vibe coding to explore the space. It will help you formulate and refine what it is you actually want to do. This is a great starting point for intent.

After your Vibe coding session (exploration) you can then use spec driven development to start to build your solutions. You can ground your specs in the outputs from your Vibe coding sessions. I have often asked my AI coding assistants to generate some draft requirements as a result of Vibe coding sessions which are ready to be used as part of a spec driven development project. 

---

## Comparing Spec Driven Development 

Depending on your software development experience, you may be reading this and thinking. This all sounds very familiar. There are some elements of spec driven development that overlap with other methodologies, so I want to share some thoughts on that in this section.


> *"SDD tells you what and why. BDD checks behaviour across the system. TDD locks in correctness at the code level. These practices work well together."* -  *Jonas Diezun*


### Test Driven Development (TDD)

Similarities:

* Both emphasize defining success criteria before implementation
* Both use an iterative red-green-refactor cycle (requirements-design-implementation)

Key Differences:

* SDD operates at a higher level of abstraction
* Includes business requirements and system design, not just test cases
* Can incorporate TDD practices within the implementation phase
* Provides broader context beyond just testing

### Waterfall

Similarities:

* Both emphasize upfront planning and documentation
* Both follow a sequential phase approach

Key Differences:

* SDD is more iterative within each phase
* Specs are designed to be living documents that evolve
* The methodology is optimized for feature-level development rather than entire projects
* Greater emphasis on AI-assisted development and collaboration

### Behavior Driven Development (BDD)

Similarities:

* Both prioritize design and planning before coding
* Both create detailed technical specifications

Key Differences:

* SDD includes explicit requirements gathering
* More structured approach to task breakdown and implementation planning
* Designed specifically for AI-assisted development workflows
* Includes specific methodologies like EARS for requirements

### Model Driven Development (MDD)

Similarities:

* Both prioritize design and planning before coding
* SDD is designed for code generation through AI coding assistants, MDD generates codes through code gen tools

Key Differences:

* SDD includes detailed technical specifications, whereas MDD is focused on the model
* MDD can be tightly coupled to a specific tool
* MDD is not focused on code directly, but building blocks (the abstraction)
* MDD requires building blocks, SDD you define what your building blocks need to be

### Prompt Driven Development (PDD)

Before closing this section it is worth noting that spec driven development is similar in many ways to Prompt Driven Development (PDD) a framework that evolved to achieve many of the same objectives of SDD. PDD looked to move beyond vibe coding and provide a way that developers could use AI coding assistants to do more complex tasks.

The key difference is that SDD pivots on well defined artifacts (for example, Requirements documents written in EARS format), whereas PDD can use more flexibly written documents markdown. PDD is driven through the AI coding assistant via the chat interface, whereas SDD is typically driven through a tool.

---

## AI-Driven Development Lifecycle (AI-DLC)

[AI-Driven Development Life Cycle (AI-DLC)](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle) holds the promise of unlocking the full potential of AI in software development. It emphasises AI-led workflows and human-centric decision-making. This follows a similar, but different three step workflow. These steps are "Inception" where you determine what to build and why, the "Construction" phase that determines how to build it, and finally the "Operations" phase where you deploy and monitor.

The AI-DLC attempts to re-imagine the broader software development lifecycle. It is worth knowing about this approach although we will not be covering it in this tutorial.

---

## Integration with existing workflows

Spec driven development is designed to complement, not replace, existing development methodologies. It can be integrated into:

* Agile Sprints: Use specs for larger user stories or epics
* Feature Branches: Create specs before starting feature development
* Vibe Coding: Use Vibe coding to experiment and generate ideas/prototypes, before creating specs from what you have learned

---

## Getting started with Kiro

In July, [Kiro](https://kiro.dev) was launched, an IDE that provided an opinionated and native approach for supporting a new workflow when using AI coding assistants - spec driven development. We are going to be using Kiro throughout this workshop. Kiro provides an opinionated UI that walks you through the specs driven development workflow.

![getting started with kiro](/images/Pasted%20image%2020260507122153.png)

Kiro simplifies working with spec driven development by integrating into its user interface how to create a spec, and then walking you through the workflow: Creating detailed requirements, selecting the right technical design, and then building the implementation plan by breaking down what is needed into a series of tasks.

### Installation

You can get started with Kiro by installing it [using this link](https://kiro.dev/docs/getting-started/installation/) It is available for Windows, Linux, and MacOS.
### Authentication

After installation, the first thing you will need is to authenticate your installation. This is required so that you can setup access to the foundation models that Kiro uses. Kiro supports a number of different ways to authenticate - for using social logins, using GitHub, or configuring it through your organisations identity provider.

You **do NOT need** an AWS account to use Kiro.

### Kiro View

When you start the Kiro IDE, you will see the left hand navigator bar that contains a number of icons. One of these is the Kiro icon which will present the Kiro sidebar, presenting the specific Kiro AI features you will be working with:

- Specs overview and management - this will list any specs in the current project workspace
- Agent Hooks management - any automations you have created (we will not cover this in this workshop as this is outside the scope of spec driven development)
- Agent Steering configuration - the is where you will configure context for your projects. These can be markdown files or Skills files that you might want to add
- MCP (Model Context Protocol) servers - this is where you can configure your MCP servers via the mcp.json configuration file, configuring them at the global or project level

### Billing

Kiro offers four distinct service tiers designed to meet different development needs. These change frequently, so you should check the [official web page for details](https://kiro.dev/docs/billing/).

When you first sign up, you will get 500 Kiro Credits. You might be wondering what a Kiro Credit is. This is the unit of consumption that Kiro uses to do work. As you start using its agentic AI capabilities, these consume credits. Kiro helps you optimise your use of credits by providing capabilities like "Auto", which uses the least expensive model for any given task it has been asked to do.
