# API Story Coach v2.0

**Version:** 2.0
**Author:** Mike Amundsen
**Maintainer:** Narrative First Labs
**License:** CC BY NC SA 4.0

---

## overview

The API Story Coach v2.0 is a teaching oriented instrument built inside the AI guided reasoning and exploration framework. It helps learners craft clear, concise API Stories using a structured, seven step workflow. These stories become the raw material for downstream tools such as ALPS, OpenAPI, AsyncAPI, and prototypes.

This edition inherits the AI Coach Baseline Context Kit v2.0 and adds session start behavior hooks and runtime behavior rules. These features ensure the coach behaves consistently across multiple LLMs, including Claude, Gemini, and ChatGPT. The goal is predictability, not theatrics.

API Stories offer a short, human readable description of purpose, data, resources, actions, and rules. The coach brings structure. The learner brings intent. The combination has a long lineage, echoing the way early scholars sketched concepts as stories before committing them to formal diagrams.

---

## purpose

This project exists to support the design and teaching of API Stories. It provides:

* a complete context kit describing the philosophy and workflow
* a portable coach that yields stable results across models
* a classic output format that is easy to read and easy to transform
* a canonical example (Task Management) for classroom and workshop use

If you want to help others learn how to shape APIs through narrative rather than guesswork, this coach gives you a place to start.

---

## features

The API Story Coach v2.0 includes:

* full alignment with the AI coach baseline context kit v2.0
* session start behavior hooks that guide the model into the workflow
* runtime behavior rules that prevent drift and preserve structure
* no invention safeguards
* a deterministic output sequence
* cross model neutrality for predictable behavior
* a teaching oriented tone
* classic Markdown output style
* the complete Task Management example

---

## the classic api story workflow

API Stories follow a simple seven step path.

1. Purpose
2. Data properties
3. Resources
4. Actions
   4b. Action details (optional)
5. Associate actions with resources
6. Rules
7. Validation summary

The coach guides learners through each step using clear, stable prompts that are friendly to any LLM.

---

## cross model behavior

To support reliable execution across Claude, Gemini, ChatGPT, and other models, the coach defines:

* a required session start pattern
* a strict no invention rule
* a step discipline rule
* a format preservation rule
* a deterministic output pattern
* a model lifetime rule allowing smooth continuation if a session resets

These guards ensure the coach behaves like a tool rather than a performer.

---

## example included

The repository includes the full Task Management API Story as the canonical example. It shows every section, every list, and a complete Validation Summary. This example is used in workshops and live instruction.

---

## how to use the coach

1. Load the API Story Coach v2.0 context kit into your preferred LLM.
2. Begin a session by stating that you want to create an API Story.
3. The coach will run the session start behavior sequence and wait for confirmation.
4. Proceed through the seven steps.
5. Review the Validation Summary.
6. Convert the story into ALPS or OpenAPI using your preferred tooling.

If a session resets or the model loses context, the coach includes hooks to re establish state.

---

## recommended teaching flow

A simple but effective approach:

* introduce the idea of API Stories and their historical lineage
* walk through the example provided
* have learners draft their own stories
* refine the work together
* show how stories transform into specifications and prototypes

This mirrors the classic pattern of demonstration, guided practice, and reflection.

---

## repository contents

* `api-story-coach-context-kit-v2.0.md`
  The complete context kit for this coach.

* `ai-coach-baseline-context-kit-v2.0.md`
  The universal baseline that all coaches inherit.

* `README.md`
  This file.

Additional teaching materials or producer oriented editions can be added as the project grows.

---

## provenance

This project is part of the Narrative First AI coaching ecosystem. It is grounded in the long tradition of treating tools as partners in thought, not replacements for the human role in design.

© 2025 amundsen.com, Inc. CC BY NC SA 4.0
