# Tool Shed Sharing Program

## Purpose

We need to track the borrowing and returning of tools in a shared community tool shed, in order to make tool usage efficient, fair, and accountable. Members can browse available tools, check them out, and return them, similar to a public library system.

---

## Data Properties

These properties define the shared vocabulary of the system and are reused across all resources and actions.

* **toolId**

  * **Description:** a unique identifier for each tool stored in the system
  * **Type:** string
  * **Example:** `"TL-1021"`

* **toolName**

  * **Description:** the name of the tool as it would appear to members
  * **Type:** string
  * **Example:** `"Cordless Drill"`

* **toolType**

  * **Description:** the category or classification of the tool (for example, drill, saw, wrench)
  * **Type:** string
  * **Example:** `"Drill"`

* **condition**

  * **Description:** the current state of the tool’s wear or usability
  * **Type:** enum [new, good, worn, broken]
  * **Example:** `"good"`

* **memberId**

  * **Description:** a unique identifier for each registered member
  * **Type:** string
  * **Example:** `"MBR-0473"`

* **memberName**

  * **Description:** the full name of the member
  * **Type:** string
  * **Example:** `"Alex Ramirez"`

* **membershipStatus**

  * **Description:** the current standing of the member account
  * **Type:** enum [active, suspended, expired]
  * **Example:** `"active"`

* **borrowDate**

  * **Description:** the date the member checks out the tool
  * **Type:** date
  * **Example:** `"2025-04-12"`

* **dueDate**

  * **Description:** the date the borrowed tool is expected to be returned
  * **Type:** date
  * **Example:** `"2025-04-19"`

* **returnDate**

  * **Description:** the date the borrowed tool is actually returned
  * **Type:** date
  * **Example:** `"2025-04-18"`

* **isOverdue**

  * **Description:** indicates whether the tool’s return is past the due date
  * **Type:** boolean
  * **Example:** `false`

* **maxBorrowDays**

  * **Description:** the maximum number of days any tool can be borrowed
  * **Type:** number
  * **Example:** `7`

* **depositRequired**

  * **Description:** identifies whether a deposit is required to borrow this tool
  * **Type:** boolean
  * **Example:** `true`

---

## Resources

Each resource represents a distinct state in the system. Every resource provides a `showHome` action for universal navigation, and every item-level resource provides a companion `view<Collection>` action.

* **Home** : The home or landing page of the API.

  * Actions: [**viewTools**](#viewtools), [**viewMembers**](#viewmembers), [**viewSharings**](#viewsharings)

* **ToolCollection** : Displays a list of all tools in the shed that can be viewed or added.

  * Actions: [**viewTool**](#viewtool), [**addTool**](#addtool), [**showHome**](#showhome)

* **ToolItem** : Shows details for a single tool, including its type, condition, and availability.

  * Actions: [**updateTool**](#updatetool), [**viewTools**](#viewtools), [**showHome**](#showhome)

* **MemberCollection** : Displays all registered members of the program.

  * Actions: [**viewMember**](#viewmember), [**addMember**](#addmember), [**showHome**](#showhome)

* **MemberItem** : Shows details for a single member, including their current status and borrowing history.

  * Actions: [**updateMember**](#updatemember), [**suspendMember**](#suspendmember), [**activateMember**](#activatemember), [**viewMembers**](#viewmembers), [**showHome**](#showhome)

* **SharingCollection** : Displays all current and past tool-borrowing transactions.

  * Actions: [**createSharing**](#createsharing), [**viewSharing**](#viewsharing), [**showHome**](#showhome)

* **SharingItem** : Displays details of a specific borrowing transaction.

  * Actions: [**closeSharing**](#closesharing), [**viewSharings**](#viewsharings), [**showHome**](#showhome)

---

## Actions

Each action expresses an intent. Actions always return a single resource and follow the navigational completeness rule.

---

### [showHome](#showhome)

Use this action to return to the **Home** resource from any other resource.

* **Inputs:** none
* **Returns:** **Home**
* **Type:** Safe

---

### [viewTools](#viewtools)

Use this action to display the list of all tools available in the system.

* **Inputs:** none
* **Returns:** **ToolCollection**
* **Type:** Safe

---

### [viewTool](#viewtool)

Use this action to view details of a single tool.

* **Inputs:** toolId (`"TL-1021"`)
* **Required:** toolId
* **Returns:** **ToolItem**
* **Type:** Safe

---

### [addTool](#addtool)

Use this action to add a new tool record to the collection.

* **Inputs:** toolName (`"Cordless Drill"`), toolType (`"Drill"`), condition (`"new"`)
* **Required:** toolName, toolType, condition
* **Returns:** **ToolItem**
* **Type:** Unsafe

---

### [updateTool](#updatetool)

Use this action to change the details of an existing tool (for example, update its condition).

* **Inputs:** toolId (`"TL-1021"`), condition (`"worn"`)
* **Required:** toolId
* **Returns:** **ToolItem**
* **Type:** Idempotent

---

### [viewMembers](#viewmembers)

Use this action to display all registered members in the system.

* **Inputs:** none
* **Returns:** **MemberCollection**
* **Type:** Safe

---

### [viewMember](#viewmember)

Use this action to retrieve information about a specific member.

* **Inputs:** memberId (`"MBR-0473"`)
* **Required:** memberId
* **Returns:** **MemberItem**
* **Type:** Safe

---

### [addMember](#addmember)

Use this action to register a new member in the system.

* **Inputs:** memberName (`"Alex Ramirez"`)
* **Required:** memberName
* **Returns:** **MemberItem**
* **Type:** Unsafe

---

### [updateMember](#updatemember)

Use this action to modify information for an existing member, such as changing their membership status.

* **Inputs:** memberId (`"MBR-0473"`), membershipStatus (`"suspended"`)
* **Required:** memberId
* **Returns:** **MemberItem**
* **Type:** Idempotent

---

### [suspendMember](#suspendmember)

Use this action to suspend a member account.

* **Inputs:** memberId (`"MBR-0473"`)
* **Required:** memberId
* **Returns:** **MemberItem**
* **Type:** Idempotent

---

### [activateMember](#activatemember)

Use this action to reactivate a suspended member account.

* **Inputs:** memberId (`"MBR-0473"`)
* **Required:** memberId
* **Returns:** **MemberItem**
* **Type:** Idempotent

---

### [viewSharings](#viewsharings)

Use this action to view all tool-sharing transactions.

* **Inputs:** none
* **Returns:** **SharingCollection**
* **Type:** Safe

---

### [viewSharing](#viewsharing)

Use this action to retrieve a specific sharing record.

* **Inputs:** sharingId (`"SHR-0015"`)
* **Required:** sharingId
* **Returns:** **SharingItem**
* **Type:** Safe

---

### [createSharing](#createsharing)

Use this action when a member borrows a tool from the shed.

* **Inputs:** memberId (`"MBR-0473"`), toolId (`"TL-1021"`), borrowDate (`"2025-04-12"`), dueDate (`"2025-04-19"`)
* **Required:** memberId, toolId, borrowDate, dueDate
* **Returns:** **SharingItem**
* **Type:** Unsafe
* **Rules:** [MemberMustBeActive](#membermustbeactive), [ToolMustBeAvailable](#toolmustbeavailable)

---

### [closeSharing](#closesharing)

Use this action when a member returns a borrowed tool, closing the transaction.

* **Inputs:** sharingId (`"SHR-0015"`), returnDate (`"2025-04-18"`)
* **Required:** sharingId, returnDate
* **Returns:** **SharingItem**
* **Type:** Idempotent
* **Rules:** [ToolConditionUpdateRequired](#toolconditionupdaterequired)

---

## Rules

* **[MemberMustBeActive](#membermustbeactive)** :

  A tool may only be borrowed by a member whose `membershipStatus` is **active**.

* **[ToolMustBeAvailable](#toolmustbeavailable)** :

  A tool can only be borrowed if it is not currently part of an open sharing record.

* **[ToolConditionUpdateRequired](#toolconditionupdaterequired)** :

  When a sharing record is closed, the tool’s condition must be reviewed and updated before it can be borrowed again.

---

## Design Notes

This story enforces **navigational completeness**: every resource offers a consistent way home (`showHome`) and every item view provides a path back to its collection (`viewCollection`).
This ensures no dead ends in the API graph, making the system self-describing and traversable by both humans and agents. The pattern supports UI generation, OpenAPI export, and LLM-driven exploration equally well.

