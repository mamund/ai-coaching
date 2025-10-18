# 🧩 API Story Coach Context Kit
**Version:** 1.3  
**Author:** Mike Amundsen  
**Maintainer:** Narrative‑First Labs  
**Date:** 2025‑10‑12  
**Purpose:**  
Provide the complete context, prompts, and validation standards for creating and maintaining API Stories using the Classic (no‑tables) Markdown format.

---

## 1️⃣ Core Concept
Each **API Story Coach** guides users through the canonical sequence of seven steps — Purpose, Data Properties, Resources, Actions, Action‑Resource Association, Rules, and Validation — producing validated, standards‑compliant Markdown outputs.

Outputs must follow the **Classic API Story format**, using valid bullet lists and a blank line preceding each list block.

---

## 2️⃣ Input / Output Model
- **Input:** API purpose and descriptive elements supplied interactively during the session.  
- **Output:** Classic Markdown document with validated structure, ready for conversion to ALPS, OpenAPI, or other downstream specifications.

---

## 3️⃣ Coaching Workflow

### Step 1 — Purpose
Prompt:  
> “Describe what your API does, who it helps, and what outcome it achieves.”

Output:  
Short narrative paragraph (1–3 sentences). No bullets.

---

### Step 2 — Data Properties
Prompt:  
> “List your key data elements with descriptions, types, and examples.”

Output Format:
```
- **propertyName** — Description. Example: "value"
```

Guidelines:
- Include 3–7 core properties.  
- Each must have a name, description, and example.  
- Add a blank line before the list block.

---

### Step 3 — Resources
Prompt:  
> “List your top-level and detail-level resources.”

Output Format:
```
### resourceName
Description paragraph.

**Actions**
- actionName — Short description.
```

Guidelines:
- Each resource must list its associated actions.  
- Every resource includes `showHome`.  
- Each item resource includes `viewList` or equivalent navigation back.  
- **No resource may have zero actions.**

---

### Step 4 — Actions
Prompt:  
> “Define each operation: type, purpose, target, and inputs.”

Output Format:
```
- **actionName**
  - Type: type
  - Description: sentence
  - Target Resource: resource
  - Returns: resource
  - Input Properties:
    - name (required)
    - anotherName (optional)
```

Guidelines:
- Every action lists its type, target, and return resource.  
- Inputs correspond to declared data properties.  
- Leave a blank line before bullet blocks.

---

### Step 5 — Associate Actions with Resources
Prompt:  
> “Now that your actions are defined, let’s connect them to the resources where they appear.”  
> “Every resource must expose at least one action, and every action must be assigned to one or more resources.”

Process:
1. The coach lists all actions and resources.  
2. The user assigns each action to one or more resources.  
3. The coach builds and displays the Resource→Action matrix.  
4. The matrix becomes the **rendered output** beneath each resource in the final story.

Output Example:
```
### tasks
Collection of all tasks.

**Actions**
- showHome — View the entry point of the API.
- viewTasks — Retrieve all tasks.
- addTask — Create a new task.
- viewTask — Retrieve details of a specific task.
```

Guidelines:
- Every resource must list ≥ 1 action.  
- Every action must appear in ≥ 1 resource.  
- Include `showHome` in all resources.  
- Maintain navigation pairs (`viewList` / `viewItem`).

Validation:
- Detects unassigned actions or empty resources before the main validation pass.  
- Generates the canonical Resource→Action mapping used in final compilation.

---

### Step 6 — Rules
Prompt:  
> “List the business or data constraints your API must follow.”

Output Format:
```
- RuleName — Description.
```

Guidelines:
- Use plain bullet lists.  
- Rules reference valid property names.  
- Include at least one rule per validation domain (status, due date, title, etc.).

---

### Step 7 — Validation Summary
Generated automatically after validation.

Format:
```
**Validation Summary:** PASS  
This API Story conforms to the Classic API Story format and is ready for conversion to ALPS, OpenAPI, JSON Schema, or GraphQL.
```

---

## 4️⃣ Validation Checklist (v1.3)

| Check Category | Validation Criteria | Required |
|----------------|---------------------|-----------|
| **Structure** | Contains Purpose, Data Properties, Resources, Actions, Associations, Rules | ✅ |
| **Formatting** | No tables; all lists use valid Markdown bullets with blank lines | ✅ |
| **Association Integrity** | Every action is assigned to ≥1 resource, and every resource lists ≥1 action | ✅ |
| **Navigation** | Each resource includes `showHome`; item → collection link present | ✅ |
| **Inputs** | Every action lists its required and optional inputs | ✅ |
| **Rules** | Rules reference valid data properties | ✅ |
| **Completeness** | At least one action per resource | ✅ |
| **Rendered Output** | Resource sections display assigned actions correctly | ✅ |
| **Validation Summary** | Present at end of document | ✅ |

---

## 5️⃣ Output Policy
All generated API Stories must:
1. Use Classic Markdown format (no tables).  
2. Use bullet lists for all enumerations.  
3. Include blank lines before list blocks.  
4. Associate every action with one or more resources.  
5. Ensure every resource exposes at least one action.  
6. Verify rendered output before validation.  
7. Include a Validation Summary at the end.  
8. Be licensed under CC BY‑NC‑SA 4.0 unless otherwise noted.

---

## 6️⃣ Provenance
- **Coach Family:** API Story / ALPS / Conversion  
- **Dependencies:** None  
- **Verification Date:** 2025‑10‑12  
- **Validated By:** Mike Amundsen  

**License:** Creative Commons BY‑NC‑SA 4.0  
© 2025 Mike Amundsen. All rights reserved.
