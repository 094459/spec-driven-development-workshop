So far we have looked at the spec workflows and the artefacts that they generate. How do we provide those specs with the right context to make sure that the output matches what we want or need? This is where we look at Context Engineering and how we can provide the right context that will help guide our specs along the right path.

## Adding Context with Steering documents

Steering documents are markdown documents that provide context to your specs. These can be scoped at the global or project level, allowing you to have control on how you want to manage this. Global steering documents for things you want to be consistent across your projects, and project level steering that is intent or project specific.

**Steering documents and intent have a close relationship**. The steering documents that you create will be aligned to the intent you have.

Steering documents have a structure: front matter where you define filters (inclusion modes) to control which steering files to use, and then the actual body of context you want to include.

Providing context is critical in getting good output from AI coding assistants, so the temptation to put everything is very real. However, you should resist this. Edit your context files ruthlessly so that they are as small as you can make them.

### Greenfield vs Brownfield

Steering documents work slightly differently depending on whether you are working on an existing code base (brownfield) or are starting a new project.
#### Brownfield

When using Kiro with an existing codebase, it can automatically generate steering files for your project. Kiro will review your project workspace, and then generate a set of foundational steering files to establish core project context: product.md, tech.md, and structure.md

- Product Overview (product.md) - Defines your product's purpose, target users, key features, and business objectives. This helps Kiro understand the "why" behind technical decisions and suggest solutions aligned with your product goals.
- Technology Stack (tech.md) - Documents your chosen frameworks, libraries, development tools, and technical constraints. When Kiro suggests implementations, it will prefer your established stack over alternatives.
- Project Structure (structure.md) - Outlines file organisation, naming conventions, import patterns, and architectural decisions. This ensures generated code fits seamlessly into your existing codebase.

It is important that you review these three artefacts after they have been generated. Check that they are accurate and reflect the project you are working on. If there are key pieces of information missing, you can edit the files and make revisions. This is important because these documents will be used throughout the workflow steps.

> **Note!** An important step to be aware of. If you do make edits and changes, make sure you ask Kiro to reload these files into its context window. If you fail to do this, it will retain the original versions in its "memory". The prompt I use is as follows (changing it based on which steering doc was updated):
> 
> "I have updated the steering document xx.md - please reload"

#### Greenfield

With a blank project, you use steering docs in a different way - to influence and guide the direction of Kiro when working through its workflow.  These are created as standard markdown text files.

Here are a few examples of steering files to give you an idea of how you can use them for your own projects.

- **API Standards (api-standards.md)** - Define REST conventions, error response formats, authentication flows, and versioning strategies. Include endpoint naming patterns, HTTP status code usage, and request/response examples.

- **Testing Approach (testing-standards.md)** - Establish unit test patterns, integration test strategies, mocking approaches, and coverage expectations. Document preferred testing libraries, assertion styles, and test file organisation.

- **Code Style (code-conventions.md)** - Specify naming patterns, file organisation, import ordering, and architectural decisions. Include examples of preferred code structures, component patterns, and anti-patterns to avoid.

- **Security Guidelines (security-policies.md)** - Document authentication requirements, data validation rules, input sanitisation standards, and vulnerability prevention measures. Include secure coding practices specific to your application.

- **Deployment Process (deployment-workflow.md)** - Outline build procedures, environment configurations, deployment steps, and rollback strategies. Include CI/CD pipeline details and environment-specific requirements.
### Filtering steering files

You can filter which context (steering) files to use by using inclusion modes which define rules that can include or exclude a steering file from being included in context. They look like this

```
---
inclusion: fileMatch
fileMatchPattern: "components/**/*.tsx"
---
```

- **Always Included** - the default mode (and where no Inclusion Mode header is provided). These files are loaded into every Kiro interaction automatically. Use this mode for core standards that should influence all code generation and suggestions. Examples include your technology stack, coding conventions, and fundamental architectural principles.
- **Conditional** - Files are automatically included only when working with files that match the specified pattern. This keeps context relevant and reduces noise by loading specialized guidance only when needed.
- **Manual** - Files are available on-demand by referencing them with #steering-file-name in your chat messages. This gives you precise control over when specialised context is needed without cluttering every interaction.

### Steering file strategies

It is tempting when thinking about what you want to include in your steering files to put everything in. Don't! Here are some strategies to help you add the right steering docs to your project.

- Always use Generate when working with existing projects and then review/edit the output for accuracy. If things are missing, add them.
- Start small and include just the core needs you want to influence
- Use the different inclusion modes to help the AI coding assistant optimise which steering files to use and optimize your context window utilisation
- Use clear and descriptive names when naming your steering files (e.g. api-rest-conventions.md - REST API standards)
- Provide examples - use code snippets, example input/outputs, style and structure guides
- Security first - make sure you do NOT include sensitive information in your steering docs. **Never include** API keys, passwords, or sensitive data
- Review and maintain your steering files as you iterate and improve them.

## Using Model Context Protocol

In addition to steering docs, Model Context Protocol (MCP) provides AI coding assistant with up to date or specialised context that will help it generate more specific outputs. There are many hundreds (if not thousands) of MCP servers available to developers to help them with generalised or very specific tasks.

> **How does this work?** You AI coding assistant will make a judgement call based on the prompt which MCP servers it might want to use. You can force this by being specific in your prompt.

You have a couple of strategies open to you as you think about how you want to incorporate the context from MCP Servers.

- Configure MCP Servers within your AI coding assistant tool
- Generate markdown steering docs from the output of running prompts against an MCP Server

The key difference between the two approaches is around how you manage what context is provided. MCP Servers can fill up the context window, and its hard to see what is being included (you are kind of at the mercy of the MCP Server). Piping the output to a markdown file and then adding this as steering can be an optimization technique. It will also allow you to review and edit what you provide - for many queries, you might actually only need a small portion of what the MCP Server might bring back. The other side however is that if the AI coding assistant needs information (context) that you did not include, you might get unexpected results. Depending on what you are doing, having the latest, up to date information might be important. These are things you need to think about.

## Agent Skills

Skills are portable instruction packages that follow the open [Agent Skills](https://agentskills.io/) standard. They bundle instructions, scripts, and templates into reusable packages that Kiro can activate when relevant to your task.

AI agents are increasingly capable, but they often lack the specific context needed for real work. Without knowledge of your team's deployment process, your company's code review standards, or your project's data analysis pipeline, agents guess and iterate — just like you would when learning something new.

Loading all this context upfront isn't practical either. Too much information overwhelms the agent, slowing responses and reducing quality. Skills solve this with progressive disclosure:

1. **Discovery** - At startup, Kiro loads only the name and description of each skill
2. **Activation** - When your request matches a skill's description, Kiro loads the full instructions
3. **Execution** - Kiro follows the instructions, loading scripts or reference files only as needed

This keeps context focused while giving Kiro access to extensive specialised knowledge on demand.
#### Skills and Spec Generation

As of writing, adding Agent Skills will not influence or steer the technical design or architecture. Skills are useful during the Implementation phase or when using the Vibe Coding mode of Kiro.