# API story to Node.js prototype context kit
Version: v0.2
Status: Functional contract baseline, includes RULES v0.3 posture

---

# 1. Purpose

This context kit defines a deterministic transformation from an API Story document into a runnable Node.js prototype.

The prototype is not production-grade. It exists to:

- faithfully project the API Story into a working HTTP service
- reflect all declared affordances (do not collapse the interface)
- enforce declared inputs, types, roles, and rules
- emit explicit hypermedia controls with explicit hrefs
- fail fast when the story is invalid

The story is the semantic authority. The generator must not infer missing intent.

---

# 2. Prototype scope

Included:

- Express-based Node.js service
- In-memory storage
- Deterministic routing by convention
- HAL-style representations
- HAL-FORMS-style _templates
- Collection responses using _embedded
- Problem-details style errors
- Optional role gating based on ROLES and AllowedRoles

Not included:

- Authentication or authorization implementations beyond lightweight role gating
- Persistence layer
- Production hardening (headers, rate limiting, performance)
- Full OpenAPI generation (may be separate output later)

---

# 3. Story authority and validation

## 3.1 Inputs and requiredness

- Stories explicitly list inputs, including id.
- Stories explicitly list query parameters such as filters.
- Do not add inputs by convention.

REQUIRED lines:

- REQUIRED is optional.
- If REQUIRED is missing, no inputs are required by default.
- If REQUIRED exists, only listed inputs are required.
- Requiredness is never inferred from action name or method.

Item-level actions:

- id MUST be in inputs
- id MUST be in REQUIRED
- Otherwise generation fails

## 3.2 Properties and types

- Types appear only in PROPERTIES.
- Action input names must reference PROPERTIES.
- RULES may reference only defined properties.
- Unused properties are allowed.
- Unknown type hints are allowed, warn and treat as string.

Canonical type hints:

- [UUID], [string], [text], [integer], [number], [boolean], [date], [datetime], [email], [url]

## 3.3 RULES posture

- RULES are natural language.
- The processor recognizes only known patterns from the RULES pattern catalog.
- Unrecognized rule lines are warnings and are not enforced.
- RULES do not imply requiredness.

Rule labels are not used.

---

# 4. ROLES contract

If ROLES is defined:

- Every resource MUST declare AllowedRoles.
- Every action MUST declare AllowedRoles.
- Every AllowedRoles value must exist in ROLES.
- No duplicate roles in ROLES or AllowedRoles.
- No inheritance or fallback behavior.

If ROLES is NOT defined:

- AllowedRoles MUST NOT appear anywhere.

Prototype enforcement expectation:

- Accept an X-Role header when ROLES is present.
- If role token is unknown, return 403.
- If role is missing and anon exists, treat as anon.
- If role is missing and anon does not exist, return 401.
- If role is not allowed for the target action, return 403.

---

# 5. Action naming and HTTP mapping

Read action prefixes:

- Get
- Show
- View

Collection-level reads:

- names ending in List or Collection
- map to GET /{plural}
- appear in _links

Item-level reads:

- GetXItem, ShowXItem, ViewXItem, also GetX, ShowX, ViewX
- map to GET /{plural}/{id}
- appear in _links

Mutation mapping:

- AddX -> POST /{plural}
- UpdateX -> PUT /{plural}/{id} (full replacement)
- SetX -> PATCH /{plural}/{id} (partial)
- RemoveX -> DELETE /{plural}/{id}

updateX convention:

- Treat as full replacement PUT
- Reject updates missing required fields for that action

setX convention:

- Treat as PATCH
- Internal multi-field patch implementation is allowed
- External interface must reflect all story-defined affordances

---

# 6. Deterministic input placement

There is no in metadata in stories.

Collection reads:
- all inputs in query

Item reads:
- id in path
- others in query

Collection mutations:
- all inputs in body

Item mutations:
- id in path
- others in body

No implicit inputs are ever added.

---

# 7. Hypermedia representation model

General:

- Every affordance includes an explicit href.
- Clients must not compose URLs.
- Affordances appear in exactly one place:
  - if no inputs, use _links
  - if inputs exist, use _templates
- DELETE affordances appear in _templates.
- AddX templates appear only on collection representations, not on HOME.
- Do not assume affordance placement by convention, the story defines which actions appear on each resource.

Home:

- Expose only story-defined affordances.
- No automatic addX.
- Include self link if story declares it.

Collection:

- Use _embedded for item representations.
- Include story-defined _links and _templates.

Item:

- Include story-defined _links and _templates.
- Use fully resolved hrefs, no {id} placeholders.

---

# 8. Mutation strictness

- Reject mutation requests that include unknown body fields.
- Empty values are valid unless a RULE forbids them.
- PATCH requests may include fields from multiple SetX affordances.
  - Validate each included field, then apply all changes in one operation.

ID handling:

- Client may supply id only when the action declares id and lists it as required.
- Conflicts return 409.
- Server generated ids use UUID style.

---

# 9. Error model

All errors use problem-details style JSON.

Status codes:

- 400 for validation failures and malformed requests
- 401 for missing role when anon is not defined (ROLES mode only)
- 403 for role not allowed or unknown role token (ROLES mode only)
- 404 for not found
- 409 for uniqueness conflicts and id conflicts

Unknown rule lines generate warnings at generation time, not runtime errors.

---

# 10. Template property details

_templates must include property details derived from story content:

- name
- required flag (from action REQUIRED list)
- type and format (from PROPERTIES type hint mapping)
- enum options (from enum RULES, when present)
- recognized constraints (min, max, length, etc.) when present

---

# 11. Output expectations

The generator should emit:

- a runnable Node.js prototype
- a visible story validation report including warnings
- deterministic routes and handlers for all story actions
- deterministic hypermedia controls for all story actions
