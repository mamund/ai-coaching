# diagramming coach v2.0

**Version:** 2.0
**Author:** Mike Amundsen
**Maintainer:** Narrative First Labs
**Based On:** AI Coach Baseline Context Kit v2.0 and AI Coach Starter Template v0.5
**License:** CC BY NC SA 4.0

The Diagramming Coach helps users see the shape of a system by turning narrative descriptions into simple Mermaid diagrams. It is a teaching tool, not a replacement for human judgment. Its job is to take the words you provide and reveal the structure that sits underneath them. Early cartographers did much the same thing, although their maps involved coastlines rather than API stories.

This coach follows the full v2.0 rules for session behavior, guidance style, validation, and workflow. It works identically across ChatGPT, Gemini, Claude, and Copilot.

---

## purpose

The Diagramming Coach helps students and practitioners visualize how resources and actions relate. It is especially useful when working with early drafts of API stories, workflows, or task sequences. The coach reads a user’s description, extracts places and actions, and produces a Mermaid diagram that captures the logic in a top to bottom flow.

---

## what this coach produces

A full coaching session results in:

* a Mermaid diagram using the grouped edge style
* a guide explaining how to read the diagram
* notes on the choices made during extraction and refinement
* a validation summary following the v2.0 baseline
* suggestions for next steps in your design process

The coach also offers a downloadable Markdown version of the final artifact.

---

## how it works

The Diagramming Coach follows the seven stage universal coaching workflow:

1. **Orientation** clarify the intent and scope
2. **Exploration** extract places, actions, and names
3. **Structure** draft the diagram
4. **Reflection** compare the picture to the intent
5. **Refinement** correct labels and flows
6. **Synthesis** produce the final output
7. **Validation** confirm completeness and offer next steps

This pattern supports clear thinking without rushing the user into conclusions. It mirrors historic reasoning practices found in early systems engineering texts, where diagrams served as the scaffolding for better thought.

---

## session start behavior

Every session begins with a short introduction explaining the AI nature and scope of the coach. The user must confirm they want to continue before Orientation begins. This ensures predictable behavior across all major LLM environments.

---

## runtime behavior

The coach clarifies during each stage what information it needs, asks before generating diagrams, and confirms labels and flows before refinement. It does not invent resources or actions. It asks for missing details when the story leaves gaps. The runtime rules follow the v2.0 baseline and the starter template.

---

## when to use this coach

Use this coach when you want to see how a system flows. It works well after writing an API story, designing user tasks, or drafting an early workflow. It also helps validate whether your story contains enough structure to support ALPS modeling or security analysis.

---

## prerequisites

You only need a list of places and the actions that connect them. They can be vague or incomplete at the start. The coach will help reveal what is missing.

---

## ecosystem placement

The Diagramming Coach sits between the API Story Coach and the ALPS Coach. It helps users confirm that their story has a coherent flow before transforming it into formal descriptors. It also provides visual support for the Vocabulary Coach, the Security Coach, and the upcoming Change Management Coach.

---

## provenance

This coach was generated using:

* AI Coach Starter Template v0.5
* AI Coach Baseline Context Kit v2.0
* Diagramming Coach v1.0 as reference material

© 2025 amundsen.com, Inc.

