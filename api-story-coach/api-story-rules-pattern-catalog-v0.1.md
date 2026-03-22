# API Story RULES Pattern Catalog
Version: v0.1
Status: Initial natural language pattern set

---

# 1. Purpose

This document defines the first recognized pattern catalog for RULES in API Story documents.

RULES are written in natural language.
The processor recognizes a limited set of deterministic patterns.
Recognized patterns are enforced at runtime.
Unrecognized patterns generate warnings and are not enforced.

The processor must never guess intent.

---

# 2. Parsing posture

General parsing principles:

- Keywords are case insensitive.
- Property names are case sensitive and must match PROPERTIES.
- Extra whitespace is ignored.
- Unknown rule lines generate warnings, not failures.
- Multiple RULES may apply to the same property.

Each rule line should apply to exactly one constraint unless explicitly defined as a cross-field rule.

---

# 3. Supported pattern groups

## 3.1 Enum rules

Pattern:

`<property> MUST BE ONE OF: value1, value2, value3`

Example:

`status MUST BE ONE OF: pending, active, completed`

Runtime behavior:

- Value must exactly match one of the listed tokens.
- Comparison is case sensitive unless otherwise specified later.
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
- Applies to integer and number type hints.

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
- Date-only comparison for [date] type.
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

## 3.7 Cross-field comparison rules (limited support)

### After another field

Pattern:

`<propertyA> MUST BE AFTER <propertyB>`

Example:

`dueDate MUST BE AFTER startDate`

Runtime behavior:

- Both properties must be present.
- Compare as date or datetime.
- Reject if condition fails.

Note: Cross-field rules are limited to simple binary comparisons in v0.1.

---

# 4. Enforcement scope

RULES apply only to:

- Inputs provided in request body
- Query parameters
- Path parameters

RULES do not:

- Infer requiredness
- Modify type hints
- Change HTTP semantics

---

# 5. Interaction with REQUIRED

If a property is not present in the request:

- REQUIRED determines presence validation.
- RULES are evaluated only if property exists.

Example:

If `title MUST NOT BE EMPTY` exists but title is not REQUIRED and not provided, no rule violation occurs.

---

# 6. Error handling

Violations return:

- HTTP 400
- Problem-details style body
- Clear reference to property and violated rule

Example structure:

{
  "type": "https://api.example.com/problems/validation-error",
  "title": "Validation failed",
  "detail": "priority must be between 1 and 5",
  "invalidParams": [
    {
      "name": "priority",
      "reason": "must be between 1 and 5"
    }
  ]
}

---

# 7. Future extensions

Not included in v0.1:

- Conditional rules (if A then B)
- Role-based rule logic
- Complex boolean expressions
- Array cardinality rules
- Dependency graphs

These may be added in later versions.

---

# 8. Status

This is the first constrained, natural language rule catalog.

It favors clarity and determinism over expressiveness.

Further iterations may expand coverage, but must preserve:

- Readability
- Explicit patterns
- No inference
- No silent interpretation

