# API Story RULES Pattern Catalog
Version: v0.2
Status: Adds UNIQUE and CASE-INSENSITIVE support

---

# 1. Purpose

This document defines the recognized natural language RULES patterns for API Story documents.

RULES are written in clear, human-readable language.
The processor recognizes a constrained set of deterministic patterns.
Recognized patterns are enforced at runtime.
Unrecognized patterns generate warnings and are not enforced.

The processor must never infer intent or invent constraints.

---

# 2. Parsing posture

General parsing principles:

- Keywords are case insensitive.
- Property names are case sensitive and must match PROPERTIES.
- Extra whitespace is ignored.
- Unknown rule lines generate warnings, not failures.
- Multiple RULES may apply to the same property.
- Each rule line represents exactly one constraint.

---

# 3. Supported pattern groups

## 3.1 Enum rules

Pattern:

`<property> MUST BE ONE OF: value1, value2, value3`

Example:

`status MUST BE ONE OF: pending, active, completed`

Runtime behavior:

- Value must exactly match one of the listed tokens.
- Comparison is case sensitive.
- Reject with 400 if value not in set.

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

---

## 3.5 Date rules

### Not in the past

Pattern:

`<property> MUST NOT BE IN THE PAST`

Example:

`dueDate MUST NOT BE IN THE PAST`

Runtime behavior:

- Compare against current date at request time.
- Date-only comparison for [date].
- Full timestamp comparison for [datetime].

### On or after today

Pattern:

`<property> MUST BE ON OR AFTER TODAY`

Runtime behavior:

- Equivalent to not in the past for date types.

---

## 3.6 Pattern match rules

Pattern:

`<property> MUST MATCH: <regex>`

Example:

`email MUST MATCH: ^[^@]+@[^@]+\.[^@]+$`

Runtime behavior:

- Evaluate regex against full string.
- Reject on non-match.

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
- Violations return 409 Conflict.

### Case-insensitive uniqueness

Pattern:

`<property> MUST BE UNIQUE CASE-INSENSITIVE`

Example:

`email MUST BE UNIQUE CASE-INSENSITIVE`

Runtime behavior:

- Values are normalized to lowercase before comparison.
- Applies only to string and text types.
- Other types ignore CASE-INSENSITIVE modifier and treat as strict equality.
- Violations return 409 Conflict.

Scope:

- Uniqueness is enforced per resource collection.
- Not global across resources.

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
- Reject with 400 if condition fails.

---

# 4. Enforcement scope

RULES apply only to:

- Path parameters
- Query parameters
- Request body fields

RULES do not:

- Infer requiredness
- Modify HTTP semantics
- Override REQUIRED lines

---

# 5. Interaction with REQUIRED

If a property is not present in the request:

- REQUIRED determines presence validation.
- RULES are evaluated only if property exists.

Example:

If `title MUST NOT BE EMPTY` exists but title is not REQUIRED and not provided, no violation occurs.

---

# 6. Error model

Validation rule violations return:

- 400 Bad Request for validation failures
- 409 Conflict for uniqueness violations

Problem-details style response body is used.

Example:

{
  "type": "https://api.example.com/problems/validation-error",
  "title": "Validation failed",
  "detail": "email must be unique",
  "invalidParams": [
    {
      "name": "email",
      "reason": "must be unique"
    }
  ]
}

---

# 7. Future extensions

Not included in v0.2:

- Conditional rules
- Role-based rule logic
- Complex boolean expressions
- Array cardinality constraints
- Computed field rules

Future additions must preserve:

- Natural language readability
- Deterministic parsing
- No inference
- No hidden normalization

---

# 8. Status

This catalog now includes uniqueness constraints with explicit comparison semantics.

The RULES grammar remains intentionally constrained and human-friendly.
