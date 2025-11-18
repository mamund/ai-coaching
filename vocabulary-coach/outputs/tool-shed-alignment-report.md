# Vocabulary Alignment Report: Tool Shed Sharing Program

**Version:** 1.0  
**Author:** Vocabulary Coach  
**Validated:** 2025-11-13  
**Coach:** Vocabulary Coach (v1.6)  
**Context Kit:** Vocabulary Coach Context Kit v1.7 (Baseline-Aligned)

---

## Purpose

This report documents the vocabulary alignment of the **Tool Shed Sharing Program API Story** to canonical Schema.org terms. Each data property has been analyzed and mapped to the most semantically appropriate vocabulary term, with confidence scoring and rationale provided.

---

## Alignment Summary

**Total Properties Analyzed:** 13  
**High Confidence Matches (≥0.85):** 10  
**Medium Confidence Matches (0.70-0.84):** 2  
**Low Confidence Matches (<0.70):** 1

---

## Detailed Alignment Results

| Property | Suggested Term | Schema.org URI | Confidence | Rationale |
|----------|---------------|----------------|------------|-----------|
| **toolId** | identifier | https://schema.org/identifier | 0.95 | Standard identifier property |
| **toolName** | name | https://schema.org/name | 0.95 | Standard name property |
| **toolType** | additionalType | https://schema.org/additionalType | 0.80 | Type classification property |
| **condition** | itemCondition | https://schema.org/itemCondition | 0.92 | Item condition property |
| **memberId** | identifier | https://schema.org/identifier | 0.95 | Standard identifier property |
| **memberName** | name | https://schema.org/name | 0.95 | Standard name property |
| **membershipStatus** | status | https://schema.org/status | 0.85 | Status property pattern |
| **borrowDate** | Date | https://schema.org/Date | 0.90 | Date property pattern |
| **dueDate** | Date | https://schema.org/Date | 0.90 | Date property pattern |
| **returnDate** | Date | https://schema.org/Date | 0.90 | Date property pattern |
| **isOverdue** | Boolean | https://schema.org/Boolean | 0.75 | Boolean status indicator (no exact match, suggest ex:isOverdue) |
| **maxBorrowDays** | duration | https://schema.org/duration | 0.80 | Represents a time duration constraint |
| **depositRequired** | Boolean | https://schema.org/Boolean | 0.70 | Boolean requirement indicator (suggest ex:depositRequired) |

---

## Recommendations

### High-Confidence Alignments (Ready to Use)

The following properties have strong semantic matches and can be adopted immediately:

* **toolId, memberId** → `schema:identifier`
* **toolName, memberName** → `schema:name`
* **condition** → `schema:itemCondition`
* **membershipStatus** → `schema:status`
* **borrowDate, dueDate, returnDate** → `schema:Date`

### Consider Custom Extensions

For the following properties, Schema.org provides only generic type matches. Consider defining custom extensions in your `ex:` namespace:

* **isOverdue** → Recommend `ex:isOverdue` (Boolean type, but domain-specific semantics)
* **depositRequired** → Recommend `ex:depositRequired` (Boolean type, but domain-specific semantics)

### Alternative Semantic Considerations

* **borrowDate** could alternatively map to `schema:startDate` (confidence: 0.88) if you want to emphasize the "start of loan period" semantics
* **dueDate, returnDate** could map to `schema:endDate` (confidence: 0.88) to emphasize "end of loan period" semantics
* **maxBorrowDays** maps well to `schema:duration` but could also be represented as a constraint using `schema:maxValue` with a time unit

---

## Namespace Declaration

For use in your annotated API Story:

```yaml
@context:
  schema: https://schema.org/
  ex: https://example.org/vocab/toolshed/
```

---

## Next Steps

1. **Review** the alignments, especially those with confidence below 0.85
2. **Apply** the suggested vocabulary references to your API Story
3. **Extend** with custom `ex:` terms where Schema.org coverage is insufficient
4. **Validate** the annotated story for completeness
5. **Continue** to other AI Coaches (ALPS, OpenAPI, JSON Schema) as needed

---

**Validation Summary:** PASS  
This alignment report conforms to the Vocabulary Coach standard and is ready for application.

© 2025 amundsen.com, Inc. Licensed CC BY-NC-SA 4.0.
