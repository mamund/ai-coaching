# API story processor update guide
Version: v0.1
Status: Rules locked from recent sessions

---

# 1. Purpose

This document describes the validation and normalization rules the API Story processor must enforce so downstream generation (ALPS, OpenAPI, Node.js prototype, etc.) is deterministic and faithful to the story.

The story is the semantic authority. The processor must not invent affordances, inputs, routes, query params, or requiredness.

---

# 2. Core concepts

## 2.1 Story sections assumed by this guide

- RESOURCES (or equivalent)
- ACTIONS (per resource)
- PROPERTIES (global property catalog)
- RULES (constraints, preferably natural language)
- Optional per action REQUIRED line

Exact section labels can vary; the processor should map the incoming format into a normalized internal form.

## 2.2 Determinism goals

- Every action can be mapped to an HTTP method and a canonical URL by rule.
- Every action input can be located deterministically (path, query, body) without adding `in:` hints.
- Every property has a resolvable type.
- Every rule is either recognized and enforced, or explicitly ignored with a warning.

---

# 3. Validation rules (fail generation)

These are hard errors. If any occur, the processor must stop and report them clearly.

## 3.1 Property catalog integrity

1. Every property in PROPERTIES MUST declare exactly one type hint (for example `[UUID]`, `[string]`, etc.).
2. Property names MUST be unique.
3. Unknown type hints are allowed (see 6.2) but must still be present as exactly one hint token.

## 3.2 Action input integrity

1. Every action input name MUST reference a property defined in PROPERTIES.
2. Any RULE that references a property MUST reference a property defined in PROPERTIES.

Unused properties are allowed.

## 3.3 Item level identifier rule

For any item level action, the story MUST include:

- `id` in the action input list
- `id` in the action REQUIRED list

If either is missing, fail.

This rule exists even if older stories did not require it; it is now the baseline.

## 3.4 Action presence per resource

Each resource MUST declare one or more actions.
If a resource has zero actions, fail.

---

# 4. Normalization rules (no invention)

These rules shape the processor output into a stable internal representation, but must not introduce new semantics.

## 4.1 Preserve declared names

- Preserve action names exactly as declared (case, spelling, etc.).
- Preserve property names exactly as declared.
- Do not normalize to camelCase or rename affordances.

## 4.2 REQUIRED line semantics

- The REQUIRED line is optional.
- If REQUIRED is missing, then no inputs are required by default.
- If REQUIRED exists, only the listed inputs are required.
- Requiredness must not be inferred from action name, method, or property type.

## 4.3 Input lists contain names only

- Type hints do not appear in action input lists.
- Types are always resolved through PROPERTIES.

---

# 5. Action naming conventions and scope

The story uses naming conventions to indicate read scope.

## 5.1 Read action prefixes

Read actions MAY use any of these prefixes:

- Get
- Show
- View

## 5.2 Collection level reads

Collection level read actions are those whose names end in:

- List
- Collection

Examples: `GetTaskList`, `ShowTaskCollection`.

## 5.3 Item level reads

Item level read actions include:

- `GetXItem`, `ShowXItem`, `ViewXItem`
- `GetX`, `ShowX`, `ViewX`

Examples: `GetTaskItem`, `ViewTask`.

## 5.4 Mutation naming conventions

- `AddX` indicates create semantics (collection mutation).
- `UpdateX` indicates full replacement update semantics.
- `SetX` indicates partial update semantics.
- `RemoveX` indicates delete semantics.

The story still decides which actions exist on which resources; naming is used only to map to HTTP behavior and endpoint shape.

---

# 6. Type hints and constraint rules

## 6.1 Canonical type hints (v0)

The processor should recognize these hints and map them consistently downstream:

- `[UUID]`
- `[string]`
- `[text]`
- `[integer]`
- `[number]`
- `[boolean]`
- `[date]`
- `[datetime]`
- `[email]`
- `[url]`

## 6.2 Unknown type hints

Unknown type hints are allowed.

- Treat as `string` for prototype generation purposes.
- Emit a warning that the hint is unknown.
- Do not fail generation.

## 6.3 Enums

Enums are modeled as RULES, not as type hints.

- Enum constraints are global per property.
- Example rule form: `status MUST BE ONE OF: pending, active, completed`

---

# 7. Deterministic HTTP mapping

This section defines how the processor should emit a normalized action model suitable for Node.js prototype generation.

## 7.1 Method mapping

- `AddX` -> POST
- `UpdateX` -> PUT (full replacement)
- `SetX` -> PATCH (partial)
- `RemoveX` -> DELETE
- `Get|Show|View...` -> GET

## 7.2 Route derivation (convention based)

The story will not include `href` values and there will be no route map file.

- Collection URL: `/{plural}` (example: `/tasks`)
- Item URL: `/{plural}/{id}` (example: `/tasks/123`)

The processor must derive these by convention and pass them downstream.

## 7.3 Input location (deterministic)

There is no `in:` attribute in the story. Use these deterministic rules:

Collection level reads:
- all inputs in query string

Item level reads:
- `id` in path
- all other inputs in query string

Collection level mutations (actions that do not include `id`):
- all inputs in body

Item level mutations (actions that include `id`):
- `id` in path
- all other inputs in body

---

# 8. Hypermedia placement rules (for the prototype generator)

These rules inform how actions become `_links` or `_templates`.

- If an action requires no inputs, represent it as a link in `_links`.
- If an action has one or more inputs (including `id`), represent it as a template in `_templates`.
- Never put the same action in both places.

Special cases:
- DELETE actions appear in `_templates` with an empty `properties` list when they require no inputs beyond `id`.
- `AddX` templates appear only on collection representations, not on HOME.
- HOME contains only affordances explicitly declared by the story, nothing is added by convention.

Collection responses use HAL embedding:
- `_embedded.{plural}: [ item representations ]`

Item representations must include fully resolved hrefs:
- `/tasks/123` rather than `/tasks/{id}`

---

# 9. Mutation strictness rules (prototype runtime contract)

These are not story parsing rules, but the processor should surface them as metadata because they influence validation and tests.

- Reject mutation requests with unknown body fields (fields not listed in the action input list).
- Update (PUT) must reject requests missing required inputs for that action.
- Empty values are allowed by default (empty string, empty array, etc.)
  - Not empty must be enforced only when an explicit RULE is recognized.
- PATCH may include fields from multiple `SetX` affordances in a single request.
  - Validate each included field against its property constraints, then apply all changes.

ID handling:
- If an action requires `id`, the client may supply it.
- If a client supplies `id` on Add and it already exists, return 409 Conflict.

ID generation:
- Server generated ids use UUID style.

---

# 10. Rule parsing posture

RULES are natural language where possible.

To stay honest and deterministic:

- Recognize a small set of rule patterns (enum, range, not empty, date not past, etc.).
- If a rule line does not match a known pattern:
  - emit a warning
  - do not enforce it at runtime
  - do not transform it into a guessed validator

This ensures the processor never invents constraints.

---

# 11. Processor output contract (suggested internal IR)

The processor should output a normalized intermediate representation containing:

- resources: name, plural name, description
- properties: name, typeHint, optional metadata
- rules: raw lines plus parsed rule objects when recognized
- actions: name, resource association, inputs, requiredInputs, method, scope (home, collection, item), routeTemplate, inputLocations

This IR is the single source of truth for downstream generators.

---

# 12. Checklist for updating the processor

- [ ] Validate PROPERTIES type hints exist and are singular.
- [ ] Validate action inputs reference PROPERTIES.
- [ ] Validate RULE references exist in PROPERTIES.
- [ ] Enforce item level `id` in inputs and REQUIRED.
- [ ] Preserve declared names exactly.
- [ ] Compute method, scope, and route from naming rules.
- [ ] Compute input locations deterministically.
- [ ] Parse known RULE patterns, warn on unknown.
- [ ] Emit normalized IR for generators.

