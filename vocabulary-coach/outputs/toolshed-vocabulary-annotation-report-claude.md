# Tool Shed Sharing API - Vocabulary Annotation Report

Version: 1.0
Author: [User]
Produced: 2025-11-14
Coach: Vocabulary Coach
Context Kit: Vocabulary Coach Context Kit v2.0

---

## Executive Summary

This vocabulary annotation report defines 18 canonical data properties for the Tool Shed Sharing API domain. The vocabulary supports a local community tool-sharing system where neighbors can check in/out tools from a shared location, with tracking for returns, condition monitoring, and repair/replacement workflows.

**Domain:** Tool Shed Sharing API
**Namespace:** `toolshed`
**Total Properties:** 18

---

## Vocabulary Entries

### Tool Properties

#### toolshed:identifier
**Canonical Name:** `toolshed:identifier`  
**Definition:** Unique identifier for a tool in the shed inventory  
**Namespace:** toolshed  
**Schema Alignment:** schema:identifier  
**Related Terms:** tool ID, tool number, inventory number  
**Example Usage:** `"TOOL-001"`, `"drill-42"`

---

#### toolshed:name
**Canonical Name:** `toolshed:name`  
**Definition:** Descriptive name or type of the tool  
**Namespace:** toolshed  
**Schema Alignment:** schema:name  
**Related Terms:** tool type, tool description, tool category  
**Example Usage:** `"Cordless Drill"`, `"24ft Extension Ladder"`, `"Circular Saw"`

---

#### toolshed:condition
**Canonical Name:** `toolshed:condition`  
**Definition:** Current physical state of the tool  
**Namespace:** toolshed  
**Schema Alignment:** schema:itemCondition  
**Related Terms:** tool state, physical condition, quality  
**Example Usage:** `"good"`, `"worn"`, `"damaged"`, `"broken"`

---

#### toolshed:status
**Canonical Name:** `toolshed:status`  
**Definition:** Current availability or workflow state  
**Namespace:** toolshed  
**Schema Alignment:** schema:availabilityStarts, schema:availabilityEnds  
**Related Terms:** availability, workflow state, tool state  
**Example Usage:** `"available"`, `"checked-out"`, `"out-for-repair"`, `"scheduled-for-replacement"`

---

#### toolshed:location
**Canonical Name:** `toolshed:location`  
**Definition:** Physical location within the tool shed  
**Namespace:** toolshed  
**Schema Alignment:** schema:location  
**Related Terms:** storage location, shelf position, physical position  
**Example Usage:** `"Shelf A3"`, `"Wall Mount 7"`, `"Storage Bin 12"`

---

#### toolshed:wearLevel
**Canonical Name:** `toolshed:wearLevel`  
**Definition:** Degree of wear on the tool (may inform repair decisions)  
**Namespace:** toolshed  
**Schema Alignment:** (custom property)  
**Related Terms:** wear degree, usage level, depreciation  
**Example Usage:** `"minimal"`, `"moderate"`, `"heavy"`, or numeric scale `1-10`

---

#### toolshed:lastInspected
**Canonical Name:** `toolshed:lastInspected`  
**Definition:** Date when tool was last inspected for condition  
**Namespace:** toolshed  
**Schema Alignment:** schema:dateModified  
**Related Terms:** inspection date, last checked, maintenance date  
**Example Usage:** `"2025-11-01"` (ISO 8601 date format)

---

### Transaction Properties

#### toolshed:checkOutDate
**Canonical Name:** `toolshed:checkOutDate`  
**Definition:** Date and time when tool was checked out by a member  
**Namespace:** toolshed  
**Schema Alignment:** schema:startDate  
**Related Terms:** borrow date, loan start, checkout time  
**Example Usage:** `"2025-11-14T09:30:00Z"` (ISO 8601 datetime)

---

#### toolshed:checkInDate
**Canonical Name:** `toolshed:checkInDate`  
**Definition:** Date and time when tool was returned to the shed  
**Namespace:** toolshed  
**Schema Alignment:** schema:endDate  
**Related Terms:** return date, loan end, checkin time  
**Example Usage:** `"2025-11-16T14:45:00Z"` (ISO 8601 datetime)

---

#### toolshed:dueDate
**Canonical Name:** `toolshed:dueDate`  
**Definition:** Expected return date for a checked-out tool  
**Namespace:** toolshed  
**Schema Alignment:** schema:expectedArrivalFrom  
**Related Terms:** expected return, deadline, return deadline  
**Example Usage:** `"2025-11-16"` (ISO 8601 date)

---

#### toolshed:returnCondition
**Canonical Name:** `toolshed:returnCondition`  
**Definition:** Condition of tool at time of return (recorded on transaction)  
**Namespace:** toolshed  
**Schema Alignment:** schema:itemCondition  
**Related Terms:** return state, returned condition, condition at return  
**Example Usage:** `"good"`, `"worn"`, `"damaged"`

---

#### toolshed:borrower
**Canonical Name:** `toolshed:borrower`  
**Definition:** Reference to the member who has checked out the tool  
**Namespace:** toolshed  
**Schema Alignment:** schema:borrower  
**Related Terms:** member reference, user, lender  
**Example Usage:** `"MEMBER-042"` (references a member identifier)

---

### Member Properties

#### toolshed:memberIdentifier
**Canonical Name:** `toolshed:memberIdentifier`  
**Definition:** Unique identifier for a community member  
**Namespace:** toolshed  
**Schema Alignment:** schema:identifier  
**Related Terms:** member ID, user ID, neighbor ID  
**Example Usage:** `"MEMBER-042"`, `"neighbor-123"`

---

#### toolshed:memberName
**Canonical Name:** `toolshed:memberName`  
**Definition:** Full name of the community member  
**Namespace:** toolshed  
**Schema Alignment:** schema:name  
**Related Terms:** user name, neighbor name, member full name  
**Example Usage:** `"Jane Smith"`, `"Robert Chen"`

---

#### toolshed:contactInfo
**Canonical Name:** `toolshed:contactInfo`  
**Definition:** Contact information for the member (email, phone, etc.)  
**Namespace:** toolshed  
**Schema Alignment:** schema:contactPoint  
**Related Terms:** contact details, email, phone, contact method  
**Example Usage:** `"jane.smith@email.com"`, `"+1-555-0123"`

---

#### toolshed:borrowingHistory
**Canonical Name:** `toolshed:borrowingHistory`  
**Definition:** Reference to past borrowing transactions for this member  
**Namespace:** toolshed  
**Schema Alignment:** (custom property)  
**Related Terms:** transaction history, loan history, usage history  
**Example Usage:** Collection/array of transaction identifiers

---

### Management Properties

#### toolshed:repairStatus
**Canonical Name:** `toolshed:repairStatus`  
**Definition:** Current state in the repair workflow  
**Namespace:** toolshed  
**Schema Alignment:** schema:orderStatus  
**Related Terms:** repair state, maintenance status, repair workflow  
**Example Usage:** `"pending"`, `"in-progress"`, `"completed"`, `"cancelled"`

---

#### toolshed:replacementStatus
**Canonical Name:** `toolshed:replacementStatus`  
**Definition:** Current state in the replacement workflow  
**Namespace:** toolshed  
**Schema Alignment:** schema:orderStatus  
**Related Terms:** replacement state, replacement workflow, order status  
**Example Usage:** `"requested"`, `"approved"`, `"ordered"`, `"received"`

---

## Validation Checklist

✓ Every term has a canonical name  
✓ Every term includes a short definition  
✓ Namespaces assigned consistently  
✓ Schema alignment provided where applicable  
✓ Example usage provided for all terms  
✓ No duplicate canonical names  
✓ Related terms identified  
✓ All ambiguities resolved

---

## Usage Notes

### Namespace Convention
All properties use the `toolshed:` namespace prefix. When implementing in APIs or schemas, this should map to a formal URI (e.g., `https://api.example.com/vocab/toolshed#`).

### Data Types
While not explicitly defined in this vocabulary report, implementers should note:
- Dates use ISO 8601 format (YYYY-MM-DD)
- Datetimes use ISO 8601 with timezone (YYYY-MM-DDTHH:MM:SSZ)
- Identifiers are strings
- Status and condition values should use controlled vocabularies (enumerations)

### Transaction Audit Trail
The distinction between `toolshed:condition` (current state) and `toolshed:returnCondition` (state at return) enables condition tracking over time and accountability for tool damage.

### Workflow States
Both `toolshed:status` and the management properties (`repairStatus`, `replacementStatus`) support workflow tracking. These should be implemented with clear state transition rules.

---

## Next Steps

This vocabulary is ready for:
1. **API Stories** - Use these terms in user story development
2. **ALPS Modeling** - Map these properties to ALPS descriptors
3. **OpenAPI Specification** - Define schemas using these canonical names
4. **Data Schema Design** - Create database schemas with consistent naming
5. **Documentation** - Reference this vocabulary in API documentation

---

Validation Summary: PASS
This output is complete and ready for next steps.

© 2025 amundsen.com, Inc. Licensed CC BY-NC-SA 4.0.
