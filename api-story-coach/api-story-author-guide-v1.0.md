# API Story Author Guide
Version: v1.0
Status: Author-facing structural guide

---

# 1. Purpose

An API Story is a structured, human-readable description of an API that can be deterministically transformed into:

- A Node.js prototype
- OpenAPI documentation
- ALPS profiles
- Test scaffolds
- Validation logic

The story is the semantic authority.

The processor does not guess.
The generator does not invent.
Everything must be explicit in the story.

---

# 2. What an API Story is

An API Story combines:

- Narrative explanation (optional)
- Structured sections (required)
- Explicit actions (affordances)
- Explicit inputs
- Explicit requiredness
- Explicit property definitions
- Optional natural-language RULES
- Optional ROLES and AllowedRoles

If the structured sections were extracted and the prose removed, the API should still be fully defined.

---

# 3. Required structural sections

At minimum, a valid API Story must contain:

## 3.1 RESOURCES

Each resource must:

- Declare a name
- Declare one or more actions
- Explicitly list which actions appear on it

No action is assumed by convention.

---

## 3.2 ACTIONS

Each action must declare:

- Name
- Inputs (explicitly listed)
- Optional REQUIRED list

Naming conventions influence HTTP mapping but do not create actions automatically.

Read prefixes:
- Get
- Show
- View

Mutation prefixes:
- Add
- Update
- Set
- Remove

Item-level actions:

- id must appear in inputs
- id must appear in REQUIRED

---

## 3.3 PROPERTIES

The PROPERTIES section defines the data model.

Each property must:

- Have a unique name
- Declare exactly one type hint
- Be referenced by action inputs

Canonical type hints include:

- [UUID]
- [string]
- [text]
- [integer]
- [number]
- [boolean]
- [date]
- [datetime]
- [email]
- [url]

Unknown type hints are allowed but treated as string.

---

# 4. REQUIRED lines

The REQUIRED line:

- Is optional
- Applies only to that action
- Lists required input property names

REQUIRED does not belong in RULES.

RULES do not imply requiredness.

---

# 5. RULES section

RULES define validation constraints in natural language.

RULES:

- Contain no labels
- One constraint per line
- Use supported patterns only
- Do not imply requiredness

Examples:

- status MUST BE ONE OF: pending, in-progress, completed
- title MUST NOT BE EMPTY
- priority MUST BE BETWEEN 1 AND 5
- email MUST BE UNIQUE CASE-INSENSITIVE

Unrecognized rules will generate warnings and will not be enforced.

---

# 6. ROLES and AllowedRoles

ROLES are optional.

If ROLES is defined:

- Every resource must declare AllowedRoles.
- Every action must declare AllowedRoles.
- AllowedRoles values must exist in ROLES.
- No inheritance occurs.

If ROLES is not defined:

- AllowedRoles must not appear anywhere.

---

# 7. Hypermedia behavior

The story defines which affordances appear on which resources.

The generator will:

- Place no-input actions in _links
- Place actions with inputs in _templates
- Emit explicit href values
- Not add affordances by convention

HOME exposes only story-defined affordances.

---

# 8. Deterministic mapping expectations

Authors do not define:

- HTTP methods
- Route templates
- Input locations

These are derived deterministically from naming conventions and structure.

Authors must define:

- Action names
- Inputs
- Required inputs
- Properties
- RULES
- Roles if used

---

# 9. Minimal example structure

Example:

## Resources

### Task Collection

Actions:
- GetTaskList
- AddTask

### Task Item

Actions:
- GetTask
- UpdateTask
- RemoveTask

## Properties

- id [UUID]
- title [string]
- status [string]
- priority [integer]
- dueDate [date]

## Rules

- status MUST BE ONE OF: pending, in-progress, completed
- title MUST NOT BE EMPTY
- priority MUST BE BETWEEN 1 AND 5

---

# 10. Common mistakes

- Forgetting id in REQUIRED for item actions
- Mixing enum and numeric models for the same property
- Putting requiredness inside RULES
- Using unsupported rule phrasing
- Declaring ROLES but omitting AllowedRoles somewhere
- Relying on implied affordances

---

# 11. Final author test

Before running the processor, ask:

- If narrative text is removed, is the API still fully defined?
- Does any section require interpretation?
- Does any rule require guessing?

If yes, revise.

---

Status: This guide describes how to author a valid API Story. The processor and generator enforce the machine contract.
