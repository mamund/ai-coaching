## **README: API Story Coach**

### Quickstart

If you want to skip all the explanations and just run with it ...

Load the `api-story-coach-context-kit` into your LLM chatbot (chatgpt, copilot, claude, gemini, etc.) and then type: `BEGIN: API Story Coaching Session`

See the completed examples for more info:

 * [task-management-api-story.md](task-management-api-story.md)
 * [tool-shed-api-story.md](tool-shed-api-story.md)
 
### Purpose

The **API Story Coach** helps you express your API as a *story* — a human-readable design artifact that describes what your API does, who it serves, and how it behaves.

It’s the **first step** in the AI Coaching ecosystem and serves as the foundation for later conversions (ALPS, OpenAPI, JSON Schema, etc.).

> Think of it as *screenwriting for APIs*: you describe scenes, characters, and actions — the coach turns them into design artifacts.

### What You’ll Learn

* How to express **Purpose**, **Data**, **Resources**, **Actions**, and **Rules** clearly
* How to structure an API design conversation around *intent* and *outcomes*
* How to generate your first **API Story** document in Markdown or YAML
* How to move from story → specification → implementation

### How to Use It

1. Open ChatGPT (or another AI platform).
2. Paste the contents of `api-story-coach-context-kit.md` into a new chat.
3. Type the trigger:

   ```
   BEGIN: API Story Coaching Session
   ```
4. Follow the guided prompts.
   The coach will ask about your API’s purpose, actors, resources, and actions.
5. When finished, the coach will output an **API Story document** — ready to use as the foundation for ALPS, OpenAPI, and beyond.

### Example Session

**You:**

> BEGIN: API Story Coaching Session

**Coach:**

> Great! Let’s start by defining your API’s purpose.
> What problem does it solve, and who benefits from it?

**You:**

> A tool-sharing app that lets neighbors lend tools to each other.

**Coach:**

> Perfect — that’s the *Tool Shed Sharing Program*.
> Let’s list the main resources (e.g., Tool, Member, BorrowRequest)...

…and so on.

The session concludes with a generated Markdown file like:

```markdown
# API Story: Tool Shed Sharing Program

## Purpose
Help neighbors lend and borrow tools within a local community.

## Resources
- Tool
- Member
- BorrowRequest

## Actions
- addTool 
- borrowTool 
- returnTool 
- removeMember 
```

### Outputs

| Type                    | Format          | Description                               |
| ----------------------- | --------------- | ----------------------------------------- |
| Story                   | Markdown / YAML | Human-readable API Story                  |
| ALPS Profile (pending) | JSON / XML      | Affordance model generated from the story |
| OpenAPI Spec (pending) | YAML            | Derived API specification                 |

### Best Practices

* Start small — describe one flow or user story first.
* Keep actions **verb-based** (`addTool`, `returnBook`, `updateStatus`).
* Use consistent naming for resources and actions.
* Let the coach handle formatting — focus on clarity and purpose.

### Next Steps

After creating your API Story:

* Use the **Vocabulary Coach** to align your property names.
* Use the **JSON Schema Coach** to formalize your data models.
* Use the **Diagramming Coach** to visualize your API graph.

### Attribution

Developed by **Mike Amundsen** as part of the *AI-Driven API Design* project.
Inspired by *Narrative-First Design*, *Hypermedia-Oriented Architecture*, and *AI-Augmented Creativity*.

