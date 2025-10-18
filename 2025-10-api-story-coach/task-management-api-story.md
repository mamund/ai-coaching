# API Story: Task Management
**Version:** 1.0  
**Author:** Mike Amundsen  
**Validated:** 2025-10-12  
**Coach:** API Story Coach (v1.0)

---

## Purpose
The Task Management API helps users manage their outstanding work in simple to-do style lists.

---

## Data Properties
- **id** — Unique identifier for the task. Example: "task-12345"
- **title** — Short, descriptive title of the task. Example: "Buy groceries"
- **description** — Detailed explanation or notes for the task. Example: "Pick up milk, eggs, and bread from the store."
- **status** — Current state of the task (e.g., pending, in-progress, completed). Example: "pending"
- **priority** — Relative importance or urgency level. Example: "high"
- **dueDate** — Date or deadline when the task should be completed. Example: "2025-10-15"
- **assignee** — Person or account responsible for the task. Example: "mike@example.com"

---

## Resources

### home
Entry point listing available affordances or navigation links.

**Actions**
- showHome — View the entry point of the API.
- viewTasks — Retrieve a list of all tasks.

---

### tasks
Collection of all tasks owned or visible to the user.

**Actions**
- showHome — View the entry point of the API.
- viewTasks — Retrieve a list of all tasks.
- addTask — Create a new task.
- viewTask — Retrieve details of a specific task.

---

### task
A single task, identified by its ID.

**Actions**
- showHome — View the entry point of the API.
- viewTask — Retrieve details of a specific task.
- updateTask — Modify an existing task.
- updateStatus — Change the status of an existing task.
- updateDueDate — Modify the due date of an existing task.
- updatePriority — Modify the priority of an existing task.
- removeTask — Delete an existing task.
- viewTasks — Retrieve a list of all tasks.

---

## Actions

- **showHome**  
  - Type: view  
  - Description: View the entry point of the API.  
  - Target Resource: home  
  - Returns: home  
  - Input Properties: none

- **viewTasks**  
  - Type: view  
  - Description: Retrieve a list of all tasks.  
  - Target Resource: tasks  
  - Returns: tasks  
  - Input Properties: none

- **viewTask**  
  - Type: view  
  - Description: Retrieve details of a specific task.  
  - Target Resource: task  
  - Returns: task  
  - Input Properties:  
    - id (required)

- **addTask**  
  - Type: add  
  - Description: Create a new task.  
  - Target Resource: tasks  
  - Returns: tasks  
  - Input Properties:  
    - title (required)  
    - description (required)  
    - status (required)  
    - priority (required)  
    - dueDate (required)  
    - assignee (optional)

- **updateTask**  
  - Type: update  
  - Description: Modify an existing task.  
  - Target Resource: task  
  - Returns: task  
  - Input Properties:  
    - id (required)  
    - Any subset of: title, description, status, priority, dueDate, assignee (optional)

- **updateStatus**  
  - Type: update  
  - Description: Change the status of an existing task.  
  - Target Resource: task  
  - Returns: task  
  - Input Properties:  
    - id (required)  
    - status (required)

- **updateDueDate**  
  - Type: update  
  - Description: Modify the due date of an existing task.  
  - Target Resource: task  
  - Returns: task  
  - Input Properties:  
    - id (required)  
    - dueDate (required)

- **updatePriority**  
  - Type: update  
  - Description: Modify the priority of an existing task.  
  - Target Resource: task  
  - Returns: task  
  - Input Properties:  
    - id (required)  
    - priority (required)

- **removeTask**  
  - Type: delete  
  - Description: Delete an existing task.  
  - Target Resource: task  
  - Returns: tasks  
  - Input Properties:  
    - id (required)

---

## Rules
- ValidStatusValues — A task’s status must be one of: pending, in-progress, or completed.
- DueDateNotPast — A task’s due date cannot be set to a date earlier than today.
- RequiredTitle — A task must have a non-empty title.
- PriorityRange — A task’s priority must be one of: low, medium, or high.
- RequiredDescription — A task must include a non-empty description.
- RequiredStatus — A task must include a valid status value.
- RequiredPriority — A task must include a valid priority value.
- RequiredDueDate — A task must include a valid due date value.

---

**Validation Summary:** PASS  
This API Story conforms to the Classic API Story format and is ready for conversion to ALPS, OpenAPI, JSON Schema, or GraphQL.

© 2025 Mike Amundsen. Licensed CC BY‑NC‑SA 4.0.
