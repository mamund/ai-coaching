# API Story RULES pattern catalog
Version: v0.3
Status: Natural language constraints, deterministic pattern recognition

---

# 1. Purpose

This document defines the recognized natural language RULES patterns for API Story documents.

RULES are written in clear, human-readable language.
The processor recognizes a constrained set of deterministic patterns.
Recognized patterns are enforced at runtime.
Unrecognized patterns generate warnings and are not enforced.

The processor must never infer intent or invent constraints.

---

# 2. Authoring rules

- RULES lines have no labels or identifiers.
- Each line expresses exactly one constraint.
- Keywords are case insensitive.
- Property names must match PROPERTIES exactly.
- Extra whitespace is ignored.
- Multiple RULES may apply to the same property.
- RULES do not imply requiredness, requiredness is expressed only via action REQUIRED lists.

---

# 3. Supported pattern groups

## 3.1 Enum rules

Pattern:

`<property> MUST BE ONE OF: value1, value2, value3`

Example:

`status MUST BE ONE OF: pending, in-progress, completed`

Runtime behavior:

- Value must exactly match one of the listed tokens.
- Comparison is case sensitive.
- Violations return 400.

---

## 3.2 Numeric range rules

### Between

Pattern:

`<property> MUST BE BETWEEN <min> AND <max>`

Example:

`priority MUST BE BETWEEN 1 AND 5`

Runtime behavior:

- Value must be >= min and <= max.
- Applies to integer and number types.
- Violations return 400.

### Greater than or equal

Pattern:

`<property> MUST BE >= <value>`

Example:

`priority MUST BE >= 1`

### Less than or equal

Pattern:

`<property> MUST BE <= <value>`

Example:

`priority MUST BE <= 5`

---

## 3.3 String emptiness rules

Pattern:

`<property> MUST NOT BE EMPTY`

Example:

`title MUST NOT BE EMPTY`

Runtime behavior:

- Value must not be null.
- Value must not be empty string.
- Whitespace-only counts as empty.
- Violations return 400.

---

## 3.4 Length rules

### Maximum length

Pattern:

`<property> LENGTH MUST BE <= <number>`

Example:

`title LENGTH MUST BE <= 120`

### Minimum length

Pattern:

`<property> LENGTH MUST BE >= <number>`

Example:

`description LENGTH MUST BE >= 10`

Runtime behavior:

- Applies to string and text types.
- Uses character count.
- Violations return 400.

---

## 3.5 Date rules

### Not in the past

Pattern:

`<property> MUST NOT BE IN THE PAST`

Example:

`dueDate MUST NOT BE IN THE PAST`

Runtime behavior:

- Compare against current date or datetime at request time.
- Date-only comparison for [date].
- Full timestamp comparison for [datetime].
- Violations return 400.

### On or after today

Pattern:

`<property> MUST BE ON OR AFTER TODAY`

Runtime behavior:

- Equivalent to not in the past for date types.
- Violations return 400.

---

## 3.6 Pattern match rules

Pattern:

`<property> MUST MATCH: <regex>`

Example:

`email MUST MATCH: ^[^@]+@[^@]+\.[^@]+$`

Runtime behavior:

- Evaluate regex against full string.
- Violations return 400.

---

## 3.7 Uniqueness rules

### Strict uniqueness

Pattern:

`<property> MUST BE UNIQUE`

Example:

`email MUST BE UNIQUE`

Runtime behavior:

- Value must not duplicate an existing value within the same resource collection.
- Comparison is strict equality.
- Applies to create and update operations.
- For update, comparison excludes the current resource id.
- Violations return 409.

Scope:

- Uniqueness is enforced per resource collection.
- Not global across resources.

### Case-insensitive uniqueness

Pattern:

`<property> MUST BE UNIQUE CASE-INSENSITIVE`

Example:

`email MUST BE UNIQUE CASE-INSENSITIVE`

Runtime behavior:

- Values are normalized to lowercase before comparison.
- Applies to string and text types.
- Other types ignore CASE-INSENSITIVE modifier and treat as strict equality.
- Violations return 409.

---

## 3.8 Cross-field comparison rules

### After another field

Pattern:

`<propertyA> MUST BE AFTER <propertyB>`

Example:

`dueDate MUST BE AFTER startDate`

Runtime behavior:

- Both properties must be present.
- Compare as date or datetime.
- Violations return 400.

Note: Cross-field rules are intentionally limited in v0.3.

---

# 4. Enforcement scope and interaction with REQUIRED

- REQUIRED determines whether a property must be present.
- RULES are evaluated only when a property is present in the request.
- RULES do not create requiredness.

Example:
If `title MUST NOT BE EMPTY` exists but title is not REQUIRED and not provided, no violation occurs.

---

# 5. Error model

- 400 for validation errors
- 409 for uniqueness conflicts
- Problem-details style response body is used

---

# 6. Unrecognized rules

If a rule line does not match a known pattern:

- emit a warning
- do not enforce it at runtime
- do not transform it into a guessed validator

This ensures the processor never invents constraints.

---

# 7. Status

This catalog is intentionally constrained.

It favors readability and determinism over expressiveness.
