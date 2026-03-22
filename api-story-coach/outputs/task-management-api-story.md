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

**AllowedRoles**: admin, user, anon

---

### tasks
Collection of all tasks owned or visible to the user.

**Actions**
- showHome — View the entry point of the API.
- viewTasks — Retrieve a list of all tasks.
- addTask — Create a new task.
- viewTask — Retrieve details of a specific task.

**AllowedRoles**: admin, user

---

### task
A single task, identified by its ID.

**Actions**
- showHome — View the entry point of the API.
- viewTask — Retrieve details of a specific task.
- updateTask — Modify an existing task.
- setStatus — Change the status of an existing task.
- setDueDate — Modify the due date of an existing task.
- setPriority — Modify the priority of an existing task.
- removeTask — Delete an existing task.
- viewTasks — Retrieve a list of all tasks.

**AllowedRoles**: admin, user

---

## Actions

- **showHome**  
  - Type: view  
  - Description: View the entry point of the API.  
  - Target Resource: home  
  - Returns: home  
  - Input Properties: none
  - AllowedRoles : admin, user, anon

- **viewTasks**  
  - Type: view  
  - Description: Retrieve a list of all tasks.  
  - Target Resource: tasks  
  - Returns: tasks  
  - Input Properties: none
  - AllowedRoles : admin, user  

- **viewTask**  
  - Type: view  
  - Description: Retrieve details of a specific task.  
  - Target Resource: task  
  - Returns: task  
  - Input Properties:  
    - id (required)
  - AllowedRoles : admin, user

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
  - AllowedRoles : admin, user  

- **updateTask**  
  - Type: update  
  - Description: Modify an existing task.  
  - Target Resource: task  
  - Returns: task  
  - Input Properties:  
    - id (required)  
    - Any subset of: title, description, status, priority, dueDate, assignee (optional)
  - AllowedRoles : admin, user  

- **setStatus**  
  - Type: update  
  - Description: Change the status of an existing task.  
  - Target Resource: task  
  - Returns: task  
  - Input Properties:  
    - id (required)  
    - status (required)
  - AllowedRoles : admin, user  

- **setDueDate**  
  - Type: update  
  - Description: Modify the due date of an existing task.  
  - Target Resource: task  
  - Returns: task  
  - Input Properties:  
    - id (required)  
    - dueDate (required)
  - AllowedRoles : admin, user  

- **setPriority**  
  - Type: update  
  - Description: Modify the priority of an existing task.  
  - Target Resource: task  
  - Returns: task  
  - Input Properties:  
    - id (required)  
    - priority (required)
  - AllowedRoles : admin, user  

- **removeTask**  
  - Type: delete  
  - Description: Delete an existing task.  
  - Target Resource: task  
  - Returns: tasks  
  - Input Properties:  
    - id (required)
  - AllowedRoles : admin  

---

## Roles
- **anon** : anonymous user (not logged in)
- **user** : identified user (logged in)
- **admin** : administrative user (logged in)

## Rules

- id MUST BE UNIQUE
- status MUST BE ONE OF: pending, in-progress, completed
- dueDate MUST NOT BE IN THE PAST
- title MUST NOT BE EMPTY
- description MUST NOT BE EMPTY
- priority MUST BE ONE OF: low, medium, high

**Validation Summary:** PASS  
This API Story conforms to the Classic API Story format and is ready for conversion to ALPS, OpenAPI, JSON Schema, or GraphQL.

© 2025 Mike Amundsen. Licensed CC BY‑NC‑SA 4.0.
