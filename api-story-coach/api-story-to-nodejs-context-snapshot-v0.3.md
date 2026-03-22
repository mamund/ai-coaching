# API Story to Node.js Prototype
Context snapshot before RULES refinement
Version: v0.3
Status: Structural contract locked, RULES grammar pending

---

# 1. Purpose

This document captures the current agreed structural contract between:

- API Story documents
- The API Story processor
- The Node.js prototype generator

This snapshot freezes all non-RULES structural decisions before deeper work begins on the RULES grammar and parsing model.

The story is the semantic authority. The processor and generator are deterministic projections of that authority.

---

# 2. Core design principles

1. No invention of semantics.
2. No inferred affordances.
3. No inferred inputs.
4. No implicit authorization behavior.
5. Explicit hypermedia controls.
6. Fail fast at generation time.
7. Strict structure, flexible evolution.

---

# 3. Story structure contract

An API Story may include:

- RESOURCES
- ACTIONS per resource
- PROPERTIES
- RULES
- Optional REQUIRED line per action
- Optional ROLES section
- Optional AllowedRoles per resource and action

Section labels may vary, but these conceptual components must be present.

---

# 4. Property rules

- Every property must declare exactly one type hint in PROPERTIES.
- Property names must be unique.
- Action inputs must reference defined properties.
- RULES may reference only defined properties.
- Unused properties are allowed.
- Unknown type hints are allowed but treated as string with warning.

Canonical type hints supported:

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

---

# 5. Action rules

## 5.1 REQUIRED line

- Optional.
- If present, only listed inputs are required.
- Requiredness must not be inferred from action name or method.

## 5.2 Item-level id rule

For any item-level action:

- id MUST appear in the input list.
- id MUST appear in REQUIRED.
- Otherwise generation fails.

## 5.3 Action naming conventions

Read prefixes:
- Get
- Show
- View

Collection-level reads end with:
- List
- Collection

Item-level reads:
- GetXItem
- ShowXItem
- ViewXItem
- GetX
- ShowX
- ViewX

Mutation conventions:
- AddX
- UpdateX
- SetX
- RemoveX

Naming determines HTTP mapping and scope only.
The story determines which actions exist.

---

# 6. Deterministic HTTP mapping

Method mapping:

- AddX → POST
- UpdateX → PUT
- SetX → PATCH
- RemoveX → DELETE
- Get, Show, View → GET

Route derivation by convention:

Collection:
- /{plural}

Item:
- /{plural}/{id}

The story never defines href values.
The generator always emits explicit hrefs.
Clients must not compose URLs.

---

# 7. Input placement rules

No in: metadata is used.

Collection reads:
- all inputs → query

Item reads:
- id → path
- others → query

Collection mutations:
- all inputs → body

Item mutations:
- id → path
- others → body

No implicit inputs are ever added.

---

# 8. Hypermedia model

Affordances appear in exactly one location:

- No inputs → _links
- Has inputs → _templates

Never both.

DELETE appears in _templates.

AddX appears only on collection representations, never on HOME.

Collection responses use HAL embedding:

{
  "_links": { },
  "_embedded": {
    "plural": [ item representations ]
  },
  "_templates": { }
}

Item representations use fully resolved href values.
No templated {id} placeholders appear in live responses.

HOME exposes only affordances explicitly declared by the story.

---

# 9. Mutation strictness

- Reject unknown body fields.
- PUT must include all required fields.
- Empty values are valid unless RULE explicitly disallows.
- PATCH may include fields from multiple SetX affordances.
- Validate each included field independently.
- Apply all valid changes in one operation.

---

# 10. ID handling

- If id is required by an action, the client may supply it.
- If client supplies id on Add and it exists, return 409 Conflict.
- Server-generated ids use UUID style.

---

# 11. Error model

Problem-details style error envelope is used.

Validation failures, rule violations, and malformed requests are treated consistently.
Exact RULES-driven error semantics will be finalized in the RULES refinement phase.

---

# 12. ROLES contract

If ROLES is defined:

- Every resource MUST declare AllowedRoles.
- Every action MUST declare AllowedRoles.
- Every AllowedRoles value must exist in ROLES.
- No duplicate role tokens allowed.
- No inheritance between resource and action.

If ROLES is NOT defined:

- AllowedRoles must not appear anywhere.

---

# 13. RULES posture

RULES are natural language where possible.

Processor behavior:

- Recognize a small set of rule patterns.
- Warn on unrecognized rule lines.
- Never invent constraints.

RULES grammar refinement is the next phase of work.

---

# 14. Processor output IR expectations

The processor should emit a normalized intermediate representation containing:

- resources
- properties
- rules
- roles, optional
- actions with:
  - inputs
  - requiredInputs
  - allowedRoles, optional
  - method
  - scope
  - routeTemplate
  - inputLocations

This IR is the single source of truth for downstream generators.

---

# 15. Status

All structural elements are locked.

The next step is formalizing RULES grammar and constraint recognition.

