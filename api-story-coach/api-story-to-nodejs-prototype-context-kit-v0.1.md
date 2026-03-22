# API Story to Node.js Prototype  
Version: v0.1  
Status: Functional specification baseline  
Purpose: Deterministic story-to-prototype generator  

---

# 1. Purpose

This project defines a deterministic transformation from an **API Story document** into a runnable **Node.js prototype**.

The prototype is not production-grade. It exists to:

- faithfully project the API Story into a working HTTP service  
- reflect all declared affordances  
- enforce declared inputs, types, and rules  
- generate explicit hypermedia controls  
- fail fast when the story is invalid  

The story is the semantic authority. The generator must not infer missing intent.

---

# 2. Prototype scope

## Included

- Express-based Node.js service
- In-memory storage
- Deterministic routing by convention
- HAL-style representations
- HAL-FORMS-style `_templates`
- Runtime validation based strictly on story content
- Explicit `href` for every affordance
- Collection responses using `_embedded`

## Not included

- Authentication or authorization
- Persistence layer
- Advanced security headers
- Rate limiting
- Full OpenAPI generation
- Production performance concerns

---

# 3. Story authority rules

The generator must never invent behavior.

## 3.1 Inputs

- Every action lists its inputs explicitly.
- The `REQUIRED:` line is optional.
- If present, it defines required inputs.
- If absent, no inputs are required.

For item-level actions:

- `id` MUST appear in the action input list.
- `id` MUST appear in `REQUIRED:`.
- If not, generation fails.

## 3.2 Properties

- Types are declared only in the `PROPERTIES` section.
- Each property must include exactly one type hint.
- Action input names must reference defined properties.
- RULES may reference only defined properties.
- Unused properties are allowed.

If any reference is invalid, generation fails.

---

# 4. Type system

## 4.1 Canonical type hints

Supported canonical hints:

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

Unknown hints:

- Treated as `string`
- Emit generation warning
- Do not fail generation

## 4.2 Enums

Enums are defined in `RULES`, not in type hints.

Example:

```
status MUST BE ONE OF: pending, active, completed
```

Rules:

- Enums are global per property.
- Enum validation applies to all actions using that property.
- Template metadata should expose enum options.

---

# 5. Action naming and HTTP mapping

## 5.1 Read actions

Recognized prefixes:

- `Get`
- `Show`
- `View`

### Collection-level reads

Names ending with:

- `List`
- `Collection`

Map to:

```
GET /xs
```

Appear in `_links`.

### Item-level reads

Names such as:

- `GetXItem`
- `GetX`
- `ShowXItem`
- `ShowX`
- `ViewXItem`
- `ViewX`

Map to:

```
GET /xs/:id
```

Appear in `_links`.

Affordance names are preserved exactly as declared.

---

## 5.2 Mutation actions

Mapping rules:

- `AddX` → `POST /xs`
- `UpdateX` → `PUT /xs/:id`
- `SetX` → `PATCH /xs/:id`
- `RemoveX` → `DELETE /xs/:id`

Additional constraints:

- `updateX` requires full replacement semantics.
- `setX` allows partial updates.
- Mixed-field PATCH is accepted.
- All mutation affordances appear in `_templates`.

---

# 6. Deterministic input placement

Input placement is derived by rule, not by `in:` declarations.

## 6.1 Collection-level reads

All inputs → query string.

Example:

```
GET /tasks?status=pending
```

## 6.2 Item-level reads

- `id` → path
- all others → query

## 6.3 Collection-level mutations

All inputs → body.

## 6.4 Item-level mutations

- `id` → path
- all others → body

No implicit inputs are ever added.

---

# 7. Hypermedia representation model

## 7.1 General rules

- Explicit `href` must appear for every affordance.
- Clients must not compose URLs.
- Affordances appear in exactly one location:
  - No input → `_links`
  - Has input → `_templates`
- DELETE operations appear in `_templates`.
- `addX` appears only on collection representations, not on home.

---

## 7.2 Home (`GET /`)

- `_links` only
- No mutation templates unless explicitly declared in story
- No automatic `addX`

---

## 7.3 Collection representation (`GET /xs`)

Structure:

```json
{
  "_links": { ... },
  "_embedded": {
    "xs": [
      { ...item representation... }
    ]
  },
  "_templates": { ... }
}
```

Rules:

- Only story-declared affordances appear.
- `addX` appears here if declared.
- Items embedded as full representations.

---

## 7.4 Item representation (`GET /xs/:id`)

Structure:

```json
{
  "id": "...",
  "propertyA": "...",
  "_links": { ... },
  "_templates": { ... }
}
```

Rules:

- Fully resolved `href`, for example `/tasks/123`
- No templated `{id}` placeholders in live responses
- No affordance duplication between `_links` and `_templates`

---

# 8. PATCH semantics

- All `setX` affordances map to `PATCH /xs/:id`.
- Each template lists only its declared input properties.
- Runtime handler accepts multiple valid fields in one request.
- Each field validated independently.
- All valid updates applied in one internal patch operation.

---

# 9. Story validation rules

Generation must fail if:

- An action references an undefined property.
- A property lacks a type hint.
- A RULE references an undefined property.
- An item-level action does not list `id` as input.
- An item-level action does not list `id` as required.

Warnings only:

- Unknown type hints.
- Unused properties.

---

# 10. Runtime validation behavior

At runtime:

- Required inputs enforced per action.
- Type validation applied per property.
- Enum validation applied per property.
- RULES constraints enforced.
- Mixed PATCH fields allowed.
- Unknown request fields rejected.

---

# 11. Storage model

- In-memory store only.
- Deterministic ID generation unless story specifies otherwise.
- Reset on restart.
- Internal store interface abstracted for future extensibility.

---

# 12. Non-goals

The prototype does not:

- Infer missing affordances.
- Infer missing inputs.
- Derive full resource shapes automatically.
- Add paging, filtering, or sorting unless story defines them.
- Impose default query parameters.
- Add hidden endpoints.

---

# 13. Design philosophy

- The story is the semantic authority.
- The generator is mechanical and deterministic.
- Hypermedia affordances are explicit.
- No interface collapsing.
- No implicit composition by clients.
- Fail fast at generation time.
- Be strict about structure, flexible about future evolution.
