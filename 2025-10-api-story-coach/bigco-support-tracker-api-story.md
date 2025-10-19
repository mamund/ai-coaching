# BigCo Support Tracker API Story

---

### Header

* **API Story:** BigCo Support Tracker API Story
* **Version:** 1.0 (Validated)
* **Date:** 2025-10-19
* **Author:** API Story Coach
* **License:** Creative Commons BY-NC-SA 4.0

---

## 1️⃣ Purpose

The purpose of this API is to help field staff at BigCo Software to track customer contacts and product support activities.

---

## 2️⃣ Data Properties

The key data elements the API handles, which often form the basis of the inputs and outputs, are:

* **id** — Unique identifier for this specific activity or contact record.
* **customerID** — Identifier that links to the **customer** resource.
* **staffID** — Identifier that links to the **staffMember** resource.
* **contactType** — What kind of activity this was (e.g., phone call, site visit, email, support ticket).
* **dateOfContact** — The date and time the interaction occurred.
* **dateOfNextContact** — The scheduled date and time for any necessary follow-up.
* **product** — The specific BigCo Software product the activity relates to.
* **summary** — A brief, one-sentence description of the purpose of the contact.
* **notes** — Detailed text about the support provided, issues discussed, or next steps.
* **status** — The current state of the activity (e.g., pending follow-up, resolved, closed).

---

## 3️⃣ Resources

Resources are the key views or entities users encounter, acting as the navigation points in the API landscape.

#### home

Entry point listing available collections and navigation links.

**Actions**

* `showHome`
* `viewActivities`
* `viewStaffMembers`
* `viewCustomers`

---

#### activities

Collection of all customer contact and support activities.

**Actions**

* `showHome`
* `viewActivities`
* `viewActivity`
* `createActivity`
* `searchActivities`

---

#### activity

A single contact or support activity identified by its ID.

**Actions**

* `showHome`
* `viewActivities`
* `viewActivity`
* `updateActivity`
* `updateActivityStatus`
* `scheduleNextContactActivity`
* `removeActivity`

---

#### customers

Collection of all customers (Companies) tracked by BigCo staff.

**Actions**

* `showHome`
* `viewCustomers`
* `viewCustomer`
* `createCustomer`

---

#### customer

Details for a single customer.

**Actions**

* `showHome`
* `viewCustomers`
* `viewCustomer`
* `updateCustomer`
* `removeCustomer`
* `searchActivities`

---

#### staffMembers

Collection of all BigCo field staff members.

**Actions**

* `showHome`
* `viewStaffMembers`
* `viewStaffMember`
* `createStaffMember`

---

#### staffMember

Details for a single staff member.

**Actions**

* `showHome`
* `viewStaffMembers`
* `viewStaffMember`
* `updateStaffMember`
* `removeStaffMember`
* `searchActivities`

---

## 4️⃣ Actions

This section lists all operations and their details, clarifying necessary inputs and the resource returned (every action returns a resource).

* **`createActivity`**
    * Type: create
    * Target Resource: activities
    * Returns: activity
    * Input Properties:
        * customerID (required)
        * staffID (required)
        * contactType (required)
        * dateOfContact (required)
        * product (required)
        * summary (required)
        * notes (optional)
        * dateOfNextContact (optional)
        * status (optional)

* **`updateActivity`**
    * Type: update
    * Target Resource: activity
    * Returns: activity
    * Input Properties:
        * summary (optional)
        * notes (optional)
        * product (optional)

* **`updateActivityStatus`**
    * Type: update
    * Target Resource: activity
    * Returns: activity
    * Input Properties:
        * status (required)

* **`scheduleNextContactActivity`**
    * Type: update
    * Target Resource: activity
    * Returns: activity
    * Input Properties:
        * dateOfNextContact (required)

* **`removeActivity`**
    * Type: delete
    * Target Resource: activity
    * Returns: activities

* **`createCustomer`**
    * Type: create
    * Target Resource: customers
    * Returns: customer
    * Input Properties:
        * customerName (required)
        * contactEmail (optional)
        * contactPhone (optional)

* **`updateCustomer`**
    * Type: update
    * Target Resource: customer
    * Returns: customer
    * Input Properties:
        * customerName (optional)
        * contactEmail (optional)
        * contactPhone (optional)

* **`createStaffMember`**
    * Type: create
    * Target Resource: staffMembers
    * Returns: staffMember
    * Input Properties:
        * staffName (required)
        * staffEmail (required)
        * staffTitle (optional)

* **`updateStaffMember`**
    * Type: update
    * Target Resource: staffMember
    * Returns: staffMember
    * Input Properties:
        * staffName (optional)
        * staffEmail (optional)
        * staffTitle (optional)

---

## 5️⃣ Rules

This section lists the business and validation constraints that ensure data and process integrity.

### Data Consistency (Enumerations)

* **requiredStatusEnum**: The `status` property must be one of: `New`, `Pending Follow-up`, `In Progress`, `Resolved`, or `Closed`.
* **requiredContactTypeEnum**: The `contactType` property must be one of: `Phone Call`, `Site Visit`, `Email`, `Support Ticket`, or `Meeting`.
* **requiredProductEnum**: The `product` property must be one of: `Billing Suite`, `Reporting Engine`, `Cloud Deployment Manager`, or `Legacy Client Portal`.

### Data Completeness

* **requiredIDLinks**: Every activity must include a valid **`customerID`** and a valid **`staffID`**.
* **requiredContactInfo**: Every activity must have a **`dateOfContact`**, **`contactType`**, and **`summary`**.
* **requiredProductLink**: Every activity must relate to a **`product`** from the approved list.

### Business Logic (Date and Status Integrity)

* **futureNextContact**: The **`dateOfNextContact`** property, if set, must always be a date and time **after** the **`dateOfContact`**.
* **statusRequiresFollowUpCheck**: If the **`status`** is set to `Pending Follow-up`, the **`dateOfNextContact`** **must** have a value.
* **resolvedStatusClearsFollowUp**: If the **`status`** is set to `Resolved` or `Closed`, the **`dateOfNextContact`** **must be empty or null**.

---

## 6️⃣ Validation Summary

**Validation Summary:** PASS

This API Story conforms to the Classic API Story format, the v1.7 context rules, and is ready for conversion to ALPS, OpenAPI, or other formats.

---
© 2025 amundsen.com, Inc. All rights reserved.
