# API Story Author Compliance Checklist
Version: v1.0
Scope: Author-side validation before running the processor

This checklist helps authors confirm their API Story will pass validation and generate a deterministic Node.js prototype.

The story is the authority. The processor does not guess.

---

# 1. Resources and actions

- [ ] Every resource declares at least one action.
- [ ] No action is assumed by convention; all actions are explicitly declared.
- [ ] Action names follow the intended naming conventions (Get, Show, View, Add, Update, Set, Remove).

Item-level actions:

- [ ] id appears in the action input list.
- [ ] id appears in the REQUIRED list.
- [ ] id is defined in PROPERTIES.

Collection-level actions:

- [ ] id is not included unless explicitly required by the story.

---

# 2. REQUIRED lines

- [ ] REQUIRED appears only when inputs must be present.
- [ ] REQUIRED includes only property names defined in PROPERTIES.
- [ ] Requiredness is not implied by RULES.
- [ ] Requiredness is not duplicated inside RULES.

---

# 3. PROPERTIES section

- [ ] Every property declares exactly one type hint.
- [ ] Property names are unique.
- [ ] All action inputs reference properties defined here.
- [ ] All RULES reference properties defined here.

---

# 4. RULES section

General:

- [ ] RULES contain no labels or identifiers.
- [ ] Each line expresses exactly one constraint.
- [ ] RULES use only supported patterns from the RULES catalog.
- [ ] No narrative or descriptive rules remain in this section.

Enums:

- [ ] Enum syntax includes colon after ONE OF.
  Example: status MUST BE ONE OF: pending, active

Ranges:

- [ ] BETWEEN rules use numeric bounds.
- [ ] >= and <= rules use numeric values only.

Strings:

- [ ] MUST NOT BE EMPTY is used instead of narrative phrasing.
- [ ] LENGTH rules specify numeric limits.

Dates:

- [ ] MUST NOT BE IN THE PAST or MUST BE ON OR AFTER TODAY used correctly.

Uniqueness:

- [ ] MUST BE UNIQUE is used intentionally.
- [ ] CASE-INSENSITIVE is included only when desired.
- [ ] Uniqueness scope is per resource collection.

Unrecognized patterns:

- [ ] No experimental rule lines remain unless warnings are acceptable.

---

# 5. ROLES section (if used)

If ROLES is defined:

- [ ] Every resource declares AllowedRoles.
- [ ] Every action declares AllowedRoles.
- [ ] All AllowedRoles values appear in ROLES.
- [ ] No duplicate roles appear in ROLES.
- [ ] No duplicate entries appear in AllowedRoles.

If ROLES is NOT defined:

- [ ] AllowedRoles does not appear anywhere.

---

# 6. Hypermedia expectations

- [ ] HOME exposes only story-defined affordances.
- [ ] AddX does not appear on HOME.
- [ ] Each affordance appears in exactly one place (_links or _templates).
- [ ] DELETE appears in _templates.
- [ ] No affordance relies on client-composed URLs.

---

# 7. Model consistency

- [ ] Enum values match property descriptions.
- [ ] Numeric vs enum models are not mixed for the same property.
- [ ] No duplicate or contradictory rules exist.
- [ ] Examples and RULES agree.

---

# 8. Final author sanity check

- [ ] If I remove all narrative prose, does the story still fully define the API?
- [ ] If I hand this to a generator, will it have to guess anything?

If any answer above is uncertain, revise before running the processor.

---

Status: Author checklist only. Machines rely on processor validation rules.
