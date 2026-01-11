# Community tool shed sharing API story

## Purpose

This API enables community members to operate a shared tool shed by purchasing tools for communal use, checking tools in and out for fixed periods of time, and arranging for a tool shed manager to ship tools for repair or replacement when needed.

---

## Data properties

The system tracks the minimum data needed to preserve meaning, history, and accountability.

### Tool

* toolId
* toolName
* toolCategory
* toolStatus
* toolCondition
* toolLocation
* acquisitionDate
* replacedByToolId

### Member

* memberId
* memberName
* contactInfo
* membershipStatus

### Checkout

* checkoutId
* toolId
* memberId
* checkoutDate
* dueDate
* returnDate

### Purchase

* purchaseId
* toolId
* purchaseDate
* purchaseSource
* purchaseCost

### Repair or replacement shipment data (embedded)

* shipmentId
* toolId
* shipmentType
* shippedDate
* returnDate
* shipmentStatus

---

## Resources

Resources represent stable views that users or agents can encounter and return to over time.

### home

Entry point that orients users and provides navigation to core collections.

### tools

A collection of all tools managed by the community tool shed.

### tool

A single tool identified by toolId.
Includes current status, condition, location, embedded repair or shipment history, and links to related checkouts.

### members

A collection of all registered community members.

### member

A single member identified by memberId.
Includes membership status and links to checkout activity.

### checkouts

A collection of recorded checkout events representing the unified lending ledger.

### checkout

A single checkout event linking one tool to one member for a fixed period of time.

---

## Actions

Actions describe what people or systems can do within this world.

### General navigation

* viewHome

### Tool related actions

* viewToolList
* viewTool
* addTool
* editTool
* changeToolStatus
* checkoutTool
* checkinTool
* repairTool

### Member related actions

* viewMembersList
* viewMember
* addMember
* editMember
* changeMemberStatus

### Checkout related actions

* viewCheckoutList
* viewCheckout

---

## Action details

Action details specify required inputs and the resource returned by each action.

### viewHome

* Returns: home
* Input properties: none

### viewToolList

* Returns: tools
* Input properties: optional filters by category, status, condition, or location

### viewTool

* Returns: tool
* Input properties: toolId

### addTool

* Returns: tool
* Input properties: toolName, toolCategory, toolCondition, toolLocation, acquisitionDate

### editTool

* Returns: tool
* Input properties: toolId, toolName, toolCategory, toolCondition, toolLocation, acquisitionDate, replacedByToolId

### changeToolStatus

* Returns: tool
* Input properties: toolId, toolStatus

### checkoutTool

* Returns: checkout
* Input properties: toolId, memberId, checkoutDate, dueDate

### checkinTool

* Returns: tool
* Input properties: checkoutId, returnDate

### repairTool

* Returns: tool
* Input properties: toolId, shipmentId, shipmentType, shippedDate, returnDate, shipmentStatus

### viewMembersList

* Returns: members
* Input properties: optional filters by membershipStatus

### viewMember

* Returns: member
* Input properties: memberId

### addMember

* Returns: member
* Input properties: memberName, contactInfo, membershipStatus

### editMember

* Returns: member
* Input properties: memberId, memberName, contactInfo, membershipStatus

### changeMemberStatus

* Returns: member
* Input properties: memberId, membershipStatus

### viewCheckoutList

* Returns: checkouts
* Input properties: optional filters by toolId, memberId, date range, or status

### viewCheckout

* Returns: checkout
* Input properties: checkoutId

---

## Rules

Rules preserve meaning and prevent invalid or conflicting operations.

### Tool rules

* A tool can only be checked out when its status allows circulation.
* A tool that is checked out cannot be checked out again until it is checked in.
* A tool marked for repair cannot be checked out.
* A tool marked as replaced cannot be checked out.
* A tool may reference at most one replacement tool.
* A replacement tool must be a valid tool in the system.

### Checkout rules

* Each checkout links exactly one tool to exactly one member.
* A checkout must record a checkout date and a due date.
* A checkout must exist before a check in can occur.
* A checkout cannot be checked in more than once.
* Repair actions initiated from a checkout must reference the associated tool.

### Member rules

* A member must be in good standing to check out tools.
* A member may have multiple active checkouts unless restricted by membershipStatus.
* Changing a member’s status does not alter historical checkout records.

### History and integrity rules

* Status changes do not erase historical records.
* Completed checkouts remain visible in the checkouts collection.
* Tool history remains traceable across replacement using replacedByToolId.
* Embedded repair or shipment information is append only and does not overwrite previous entries.

---

## Validation summary

Validation Summary: PASS

This API Story includes:

* A clear purpose
* Complete data properties
* Stable resources with no dead ends
* Actions and action details with explicit returns
* Rules that preserve meaning and history

The story conforms to the Classic API Story style and is ready for conversion into ALPS, OpenAPI, AsyncAPI, or prototype implementations.

---

## Next steps

* Generate an ALPS profile using resources as states and actions as affordances.
* Optionally enumerate toolStatus values during specification or schema generation.
* Produce a hypermedia mock to test navigation and lifecycle transitions.

If you want, I can also provide a **downloadable ZIP** containing this Markdown file plus a matching ALPS profile and a simple navigation diagram.

