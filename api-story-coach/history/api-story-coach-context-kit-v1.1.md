# 🧩 API Story Coach Context Kit
**Version:** 1.1  
**Author:** Mike Amundsen  
**Maintainer:** Narrative‑First Labs  
**Date:** 2025‑10‑12  
**Purpose:**  
Provide the complete context, prompts, and validation standards for creating and maintaining API Stories using the Classic (no‑tables) Markdown format.

---

## 1️⃣ Core Concept
Each **API Story Coach** guides users through the five canonical sections of an API Story — Purpose, Data Properties, Resources, Actions, and Rules — producing validated, standards‑compliant Markdown outputs.

Outputs must follow the **Classic API Story format**, with valid bullet lists and a blank line preceding each list block.

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

### Step 5 — Rules
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

### Step 6 — Validation Summary
Generated automatically after validation.

Format:
```
**Validation Summary:** PASS  
This API Story conforms to the Classic API Story format and is ready for conversion to ALPS, OpenAPI, JSON Schema, or GraphQL.
```

---

## 4️⃣ Validation Checklist (v1.1)

| Check Category | Validation Criteria | Required |
|----------------|---------------------|-----------|
| **Structure** | Contains Purpose, Data Properties, Resources, Actions, Rules | ✅ |
| **Formatting** | No tables; all lists use valid Markdown bullets with blank lines | ✅ |
| **Navigation** | Each resource includes `showHome`; item → collection link present | ✅ |
| **Inputs** | Every action lists its required and optional inputs | ✅ |
| **Rules** | Rules reference valid data properties | ✅ |
| **Completeness** | At least one action per resource | ✅ |
| **Validation Summary** | Present at end of document | ✅ |

---

## 5️⃣ Output Policy
All generated API Stories must:
1. Use Classic Markdown format (no tables).  
2. Use bullet lists for all enumerations.  
3. Include blank lines before list blocks.  
4. Include a Validation Summary at the end.  
5. Be licensed under CC BY‑NC‑SA 4.0 unless otherwise noted.

---

## 6️⃣ Provenance
- **Coach Family:** API Story / ALPS / Conversion  
- **Dependencies:** None  
- **Verification Date:** 2025‑10‑12  
- **Validated By:** Mike Amundsen  

**License:** Creative Commons BY‑NC‑SA 4.0  
© 2025 Mike Amundsen. All rights reserved.
