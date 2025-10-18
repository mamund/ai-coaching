# 🧩 API Story Coach Context Kit v1.6 (Self-Contained Teaching Edition)

**Version:** 1.6
**Author:** Mike Amundsen
**Maintainer:** Narrative-First Labs
**Date:** 2025-10-12
**Purpose:**
Provide the complete, beginner-friendly, self-contained coaching framework for designing and validating API Stories using the **Classic Markdown** format.
This edition includes a full example (*Task Management API Story*) and instructor guidance for workshops.
It inherits all pedagogical conventions from the **AI Coach Baseline Context Kit v1.6 (Universal Template)**.

---

### Table of Contents

1. Preface
2. Introduction for First-Time Users
3. The API Story Concept
4. Seven-Step Coaching Workflow
5. Action–Resource Association Rules
6. Validation Checklist
7. Output Policy
8. Classic API Story Output Style
9. Example: Task Management API Story (with Validation Summary)
10. Instructor Notes
11. Provenance

---

## Preface

This *Self-Contained Teaching Edition* of the **API Story Coach Context Kit** is designed for onboarding, live instruction, and self-guided learning.

It combines the full API Story coaching workflow with a complete worked example to demonstrate each section in practice.
Educators and learners can use this edition to understand both *how* the API Story process works and *why* each design decision matters.

---

## 1️⃣ Introduction for First-Time Users

An **API Story** is a short narrative that describes what an API does, what information it handles, and what people or systems can do with it.
You don’t need prior API experience—just describe purpose, data, and actions.
When finished, you’ll have a clear, readable artifact that can later be converted automatically into specifications like ALPS or OpenAPI.

---

## 2️⃣ The API Story Concept

An API Story models an API as a *story about interaction* rather than a list of endpoints.
It captures:

* **Purpose** – Why the API exists.
* **Data Properties** – The key pieces of information.
* **Resources** – The views or entities users encounter.
* **Actions** – What users or agents can do.
* **Rules** – The constraints that keep the system valid.

---

## 3️⃣ Seven-Step Coaching Workflow

1. **Purpose** – Describe the API’s goal, audience, and outcome.
2. **Data Properties** – List key data elements with examples.
3. **Resources** – Define main views (home, collections, items).
4. **Actions** – Describe operations users can perform.
5. **Associate Actions with Resources** – Map where each action appears.
6. **Rules** – List business and validation constraints.
7. **Validation Summary** – Confirm readiness for conversion.

Plain-language prompts help beginners (e.g., *“What can someone do here?”*).
Each generated section includes a short explanatory paragraph except Purpose.

---

## 4️⃣ Action–Resource Association Rules

* Every resource must expose ≥ 1 action.
* Every action must appear on ≥ 1 resource.
* Include `showHome` in all resources.
* Maintain navigation pairs (`viewList` ↔ `viewItem`).
* Association integrity is checked before final validation.

---

## 5️⃣ Validation Checklist

| Category              | Check                                                           | Required |
| --------------------- | --------------------------------------------------------------- | -------- |
| Structure             | Contains Purpose, Data, Resources, Actions, Associations, Rules | ✅        |
| Formatting            | Uses bulleted lists with blank lines                            | ✅        |
| Association Integrity | No orphan actions or empty resources                            | ✅        |
| Navigation            | Includes `showHome` and return actions                          | ✅        |
| Inputs                | Each action lists required and optional fields                  | ✅        |
| Rules                 | Each rule references valid properties                           | ✅        |
| Rendered Output       | Resources display associated actions                            | ✅        |
| Validation Summary    | Present and formatted                                           | ✅        |

---

## 6️⃣ Output Policy

1. Classic Markdown (no tables).
2. Bullet lists for all enumerations.
3. Blank line before each list block.
4. Auto-render explanatory introductions (except Purpose).
5. Include Header and Footer blocks in every output.
6. Footer must use © amundsen.com, Inc.
7. License: CC BY-NC-SA 4.0.

---

## 7️⃣ Classic API Story Output Style

Each API Story is rendered as a narrative document with the following sections:

1. Purpose
2. Data Properties
3. Resources
4. Actions
5. Rules
6. Validation Summary

Bulleted lists and brief explanatory paragraphs keep the story human-readable.

---

## 8️⃣ Example: Task Management API Story (with Validation Summary)

### Purpose

The Task Management API helps users manage their work as simple to-do lists.

### Data Properties

* **id** — Unique identifier for the task.
* **title** — Short title of the task.
* **description** — Details about the task.
* **status** — Current state (e.g., pending, in-progress, done).
* **priority** — Relative importance (low, medium, high).
* **dueDate** — Date the task is due.
* **owner** — User responsible for the task.

### Resources

#### home

Entry point listing available collections and navigation links.

**Actions**

* showHome — View the entry point of the API.
* viewTasks — List all tasks.

---

#### tasks

Collection of all tasks visible to the user.

**Actions**

* showHome — View the entry point of the API.
* viewTasks — Retrieve the task list.
* addTask — Create a new task.
* viewTask — View details of a specific task.

---

#### task

A single task identified by its ID.

**Actions**

* showHome — Return to API entry point.
* viewTask — Retrieve task details.
* updateTask — Modify an existing task.
* updateStatus — Change the status of a task.
* updateDueDate — Change the due date of a task.
* updatePriority — Change the priority of a task.
* removeTask — Delete an existing task.
* viewTasks — Return to task collection.

---

### Actions

* **addTask**

  * Type: create
  * Target Resource: tasks
  * Returns: task
  * Input Properties:

    * title (required)
    * description (optional)
    * priority (optional)
    * dueDate (optional)

* **updateTask**

  * Type: update
  * Target Resource: task
  * Returns: task
  * Input Properties:

    * title (optional)
    * description (optional)
    * priority (optional)
    * status (optional)
    * dueDate (optional)

* **removeTask**

  * Type: delete
  * Target Resource: task
  * Returns: tasks

* **updateStatus**

  * Type: update
  * Target Resource: task
  * Returns: task
  * Input Properties:

    * status (required)

* **updateDueDate**

  * Type: update
  * Target Resource: task
  * Returns: task
  * Input Properties:

    * dueDate (required)

* **updatePriority**

  * Type: update
  * Target Resource: task
  * Returns: task
  * Input Properties:

    * priority (required)

---

### Rules

* requiredTitle — Every task must have a title.
* requiredStatus — Every task must have a status.
* requiredPriority — Every task must have a priority value.
* requiredDueDate — Every task must have a due date.

---

### Validation Summary

**Validation Summary:** PASS
This API Story conforms to the Classic API Story format and is ready for conversion to ALPS, OpenAPI, or other formats.

---

## 9️⃣ Instructor Notes

**Recommended Workshop Flow**

1. Explain API Stories and why they matter (10 min).
2. Walk through the Task Management example (20 min).
3. Participants draft their own API Story (30 min).
4. Group discussion and reflection (10 min).
5. Show how stories convert to ALPS/OpenAPI (10 min).

**Tips**

* Stress intent over implementation.
* Encourage iteration.
* Reinforce that clarity beats completeness early on.
* Connect API Story ideas to UX concepts like flows and affordances.

---

## 🔟 Provenance

* **Baseline Template:** AI Coach Baseline Context Kit v1.6 (Universal Template)
* **Coach Name:** API Story Coach Context Kit v1.6 (Self-Contained Teaching Edition)
* **Verification Date:** 2025-10-12
* **Validated By:** Mike Amundsen

---

**License:** Creative Commons BY-NC-SA 4.0
© 2025 amundsen.com, Inc. All rights reserved.

