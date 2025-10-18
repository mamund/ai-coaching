## AI Coaching for API Design

### Overview

This repository hosts a growing collection of **AI Coaches**—interactive, in-chat assistants designed to help developers, designers, and architects **build better APIs** using **narrative-first, affordance-aware, and standards-based techniques**.

Each coach is a *context kit* (a self-contained Markdown file) that can be loaded into an AI chat platform such as ChatGPT, Claude, or Copilot. Once loaded, the coach provides guided, repeatable workflows that transform your ideas into high-quality API artifacts.

### Why AI Coaching?

Most API design tools assume you already know what to build.
AI Coaches help you **discover, not just describe** your API.

They:

* Guide you through a structured reasoning process (purpose → resources → actions → rules → deliverables).
* Teach you **API design as a conversation**—the way humans already think and collaborate.
* Turn raw ideas into production-ready design artifacts (e.g., ALPS, OpenAPI, AsyncAPI, JSON Schema).
* Preserve human creativity while using AI to accelerate mechanical steps.

In short:

> AI Coaches **augment** the design process — they don’t replace it.

### How It Works

Each coach includes:

1. **A Context Kit (Markdown)** – loaded into an AI chat to set up rules, structure, and personality.
2. **A Guidance Flow** – the dialogue format that keeps sessions structured and consistent.
3. **Deliverables** – API artifacts generated from the conversation (e.g., API Stories, ALPS, OpenAPI).

### Available Coaches

| Coach                 | Purpose                                                                   | Typical Deliverables                    |
| --------------------- | ------------------------------------------------------------------------- | --------------------------------------- |
| **API Story Coach**   | Capture the *narrative* of your API — who it’s for, what it does, and why | API Story (Markdown/YAML), ALPS Profile |
| **Vocabulary Coach**  | Align your property names with shared vocabularies                        | Schema alignment report, JSON output    |
| **JSON Schema Coach** | Generate and refine JSON Schema from Stories                              | JSON Schema (draft 2020-12), examples   |
| **Diagramming Coach** | Visualize resource–action relationships                                   | Mermaid diagrams, relationship graphs   |

*(More coming soon — AsyncAPI, OKR/KPI, Composable Service Design, etc.)*

### Requirements

* Any modern AI chat interface (e.g., ChatGPT, Claude, Copilot, etc.)
* No coding setup required
* Optional: Node.js for running the out-of-chat utilities (when provided)

### Responsible Use

AI Coaches run on public LLM platforms.
Do **not** share any personal, private, or company-confidential data during sessions.
These tools are designed for **education, exploration, and responsible experimentation** only.

For more, see [`Ethics and Safety`](./ethics-and-safety/).

### Getting Started

1. Open your AI chat platform (ChatGPT, Claude, etc.)
2. Copy-paste the contents of the chosen coach’s `.md` file into a new chat
3. Begin your session using the **BEGIN** trigger noted in each file

Example:

```
BEGIN: API Story Coaching Session
```

The AI will walk you through the process step-by-step.

