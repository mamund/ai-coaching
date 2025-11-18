# 🧩 Vocabulary Coach Context Kit  
**Version 1.3 — 2025-10-08**  
**Author:** Mike Amundsen  

**Purpose:**  
Provide a complete, reproducible environment for the **Vocabulary Coach**, which aligns API Story data properties to canonical vocabularies (e.g., Schema.org).  
This kit distinguishes between **in-chat coaching** (interactive) and **out-of-chat build work** (Node.js).

---

## 1️⃣ Core Concept

| Mode | Environment | Description |
|------|--------------|--------------|
| 🧠 **In-Chat Coaching** | Inside ChatGPT or any LLM | The coach analyzes API Stories (Markdown or YAML) and aligns property terms to canonical vocabulary entries from a pre-built `schemaorg-index.json`. |
| ⚙️ **Out-of-Chat Build Work** | Local Node.js environment | Used to generate or refresh `schemaorg-index.json` from the canonical Schema.org TTL file. |

---

## 2️⃣ Required Files by Mode

| File | In-Chat Coaching | Out-of-Chat Build | Description |
|------|------------------|------------------|--------------|
| `schemaorg-index.json` | ✅ | ✅ (output) | Flattened, ready-to-use vocabulary index |
| `api-story.md` / `api-story.yaml` | ✅ | ❌ | The API Story document to align |
| `schemaorg-current-https.ttl` | ❌ | ✅ | Canonical Schema.org vocabulary (RDF/Turtle) |
| `index.js` | ❌ | ✅ | Node.js build script (verified) |

---

## 3️⃣ In-Chat Coaching Workflow

### Files Needed
- `schemaorg-index.json`  
- API Story (`.md` or `.yaml`)

### Steps
1. Upload the JSON index and your story.  
2. Ask:  
   > “Run the Vocabulary Coach alignment report.”  
3. Review results.  
4. Optionally request:  
   > “Annotate the story with `vocabRef` fields.”

### Output
- Alignment Report (property → URI, confidence, rationale)  
- Annotated Story in the same format (Markdown → Markdown, YAML → YAML)

---

## 4️⃣ Input Format Specification (API Stories)

The Coach accepts both Markdown and YAML and auto-detects format.

### ✅ Markdown
```markdown
## Data Properties
* **memberId**
  * **Description:** a unique identifier for each member
  * **Type:** string
```

### ✅ YAML
```yaml
properties:
  - name: memberId
    description: a unique identifier for each member
    type: string
```

### 🧠 Processing Pipeline
1. Normalize input (Markdown → JSON, YAML → direct).  
2. Lookup each property in `schemaorg-index.json`.  
3. Generate alignment table and annotated output.

---

## 5️⃣ Prompt Template (In-Chat Mode)

**System Instruction**
> You are the *Vocabulary Coach*.  
> Accept API Stories in Markdown or YAML.  
> Extract data properties, compare each to the provided vocabulary index, and suggest canonical Schema.org URIs or `ex:` extensions.  
> Produce both a table and an annotated story in the same format.

**User Prompt Example**
```yaml
Vocabulary index: schemaorg-index.json
API Story:
  properties:
    - name: memberId
      description: a unique identifier for each registered member
```

**Expected Output**
```yaml
results:
  - property: memberId
    suggestedTerm: https://schema.org/identifier
    confidence: 0.95
    comment: Exact semantic match
```

---

## 6️⃣ Out-of-Chat Build Workflow (Verified Code)

### Prerequisites
- Node.js ≥ 18  
- Latest Schema.org TTL file (`schemaorg-current-https.ttl`)

### ✅ Verified Build Script — *index.js (2025-10-08)*

```js
/**
 * index.js  — Verified Schema.org Index Builder
 *
 * Usage:
 *   node index.js schemaorg-current-https.ttl
 *
 * Produces:
 *   schemaorg-index.json
 */

import rdf from 'rdf-ext'
import { fromFile } from 'rdf-utils-fs'
import namespace from '@rdfjs/namespace'
import fs from 'fs'

const inputFile = process.argv[2] || 'schemaorg-current-https.ttl'
const outputFile = 'schemaorg-index.json'

// Namespaces
const SCHEMA = namespace('https://schema.org/')
const RDFS   = namespace('http://www.w3.org/2000/01/rdf-schema#')
const RDF    = namespace('http://www.w3.org/1999/02/22-rdf-syntax-ns#')

console.log(`Loading ${inputFile} ...`)
const dataset = await rdf.dataset().import(fromFile(inputFile))
console.log(`Parsed ${dataset.size} triples`)

const index = {}

// Collect all labeled subjects (classes + properties)
for (const quad of dataset.match(null, RDFS.label)) {
  const subject = quad.subject
  const label   = quad.object.value
  const uri     = subject.value

  // Collect optional data
  const comment = [...dataset.match(subject, RDFS.comment)]
    .map(q => q.object.value)[0] || ''

  const domains = [...dataset.match(subject, SCHEMA.domainIncludes)]
    .map(q => q.object.value.split('/').pop())

  const ranges = [...dataset.match(subject, SCHEMA.rangeIncludes)]
    .map(q => q.object.value.split('/').pop())

  const superClasses = [...dataset.match(subject, RDFS.subClassOf)]
    .map(q => q.object.value.split('/').pop())

  const supersededBy = [...dataset.match(subject, SCHEMA.supersededBy)]
    .map(q => q.object.value.split('/').pop())

  // Store compact record
  index[label] = {
    uri,
    label,
    description: comment,
    domain: domains,
    range: ranges,
    subClassOf: superClasses,
    supersededBy
  }
}

// Write JSON file
fs.writeFileSync(outputFile, JSON.stringify(index, null, 2))
console.log(`✅ Wrote ${Object.keys(index).length} terms to ${outputFile}`)
```

### Build Command
```bash
node index.js schemaorg-current-https.ttl
```

### Output
`schemaorg-index.json` — complete flattened vocabulary index used for all in-chat alignment.

### Provenance
**Verified by:** Mike Amundsen  
**Date:** 2025-10-08  
**Enhancements:** Adds `subClassOf` and `supersededBy` for richer semantics.  
**Status:** Canonical generator for Vocabulary Coach v1.3

---

## 7️⃣ Namespace Policy

```yaml
@context:
  schema: https://schema.org/
  ex: https://example.org/vocab/
```

Use:
- `schema:` → shared / standardized terms  
- `ex:` → project-specific extensions  

---

## 8️⃣ Recommended Mappings

| Pattern | Schema.org Term | Example |
|----------|-----------------|----------|
| Unique IDs | `schema:identifier` | toolId, memberId |
| Names | `schema:name` | toolName, memberName |
| Category | `schema:category` | toolType |
| Condition | `schema:itemCondition` | condition |
| Dates | `schema:startDate`, `schema:endDate`, `schema:dueDate` | borrowDate, returnDate, dueDate |

---

## 9️⃣ Runtime vs. Build-Time Requirements

### 🧠 In-Chat Coaching (Runtime)
**Files:** `schemaorg-index.json`, `api-story.md` / `api-story.yaml`  
**Tools:** none  
**Purpose:** semantic alignment and annotation  

### ⚙️ Out-of-Chat Build (Maintenance)
**Files:** `schemaorg-current-https.ttl`, `index.js`  
**Tools:** Node.js ≥ 18  
**Purpose:** regenerate or refresh the vocabulary index  

| Action | Needs Node.js? | Needs TTL? | Needs LLM? | Output |
|---------|----------------|-------------|-------------|---------|
| Run Vocabulary Coach | ❌ | ❌ | ✅ | Alignment + annotated story |
| Rebuild Index | ✅ | ✅ | ❌ | schemaorg-index.json |
| Merge/extend vocabularies | ✅ | ✅ | ❌ | Extended index |
| Replay coaching/demo | ❌ | ❌ | ✅ | Coaching transcript |

---

## 🔟 Version & Initialization

**Vocabulary Source:** Schema.org (latest TTL)  
**Coach Version:** 1.3  
**Namespace Policy:** `schema:` for shared terms, `ex:` for local extensions  
**Quick-Start Prompt:**
> “Initialize Vocabulary Coach using `schemaorg-index.json`.  
> I’ll upload an API Story (Markdown or YAML); run the alignment report and produce the annotated story with `vocabRef` fields.”
