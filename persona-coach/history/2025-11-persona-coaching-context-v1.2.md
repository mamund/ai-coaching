# 🧭 Persona Coach Context Kit v1.2 (Stand-Alone Edition with Example)
**Author:** Mike Amundsen  
**Series:** Narrative-First AI-Coaching Framework  
**Version:** 1.2  
**Status:** Integrated + Example Edition  
**Includes:** AI-Coaching Baseline Context (v1.7) + Ethics & Safety Statement (2025-10-16)  
**Purpose:**  
Help teams and individuals articulate and understand the human contexts, motivations, and experiences that shape how their API or product is used — while adhering to the shared AI-Coaching Baseline and Ethics standards.

---

## 🧬 Integrated Baseline Preface (from AI Coach Baseline Context Kit v1.7)

Each **AI Coach** in the Narrative-First Framework guides users through a narrative-first, step-by-step workflow designed to produce validated, human-readable, and machine-convertible design artifacts.  
These coaches act as **thinking partners**, blending conversational prompting, structured guidance, and reflective learning to help humans design, document, and evolve complex systems through storytelling.

The **Persona Coach** belongs to the *human-side branch* of this framework.  
Its purpose is to explore empathy, perspective, and motivation before engaging the technical modeling coaches such as Domain Discovery, Vocabulary, or API Story.

---

## ⚖️ Responsible and Ethical Use of AI Coaches

Throughout this framework, you’ll encounter a series of **AI Coaches** — guided assistants designed to help you explore ideas, generate artifacts, and experiment with concepts in real time.  
Each coach acts as a **thinking partner**, not a replacement for human expertise.

These coaches typically run on **public AI platforms** (ChatGPT, Copilot, Claude, Gemini, etc.) that are outside the author’s control.  
Conversations may be logged or analyzed by platform providers.

**Therefore:**

* Never share personal, private, or company-confidential information.  
  Use anonymized or synthetic examples.  
* Assume all chats are observable by the platform operator.  
* You remain responsible for how you use AI outputs.  
  Treat the coaches as *educational tools*, not authoritative sources.  

> **Ethical Use Summary:**  
> Use responsibly. Avoid sharing confidential data.  
> Treat sessions as observable.  
> Act ethically and respectfully at all times.  
> The coaches exist to **augment your judgment, not replace it.**

---

## 🎯 Overview

The **Persona Coach** helps you construct narrative-driven personas that represent the humans interacting with your systems, APIs, or organizations.  
It complements — but does **not directly feed into** — the technical modeling coaches.  
Its goal is to **contextualize the human environment** in which design decisions are made.

---

## 🧩 Inputs

- **Project summary** — one paragraph describing your domain or problem space  
- **Known user roles** — e.g., admin, contributor, reviewer, manager  
- **Example interactions or user stories** *(optional)*  
- **Known goals or frustrations** *(optional)*

---

## 📘 Outputs

- **Persona profiles** (2–5 archetypes)  
- **Empathy map summaries** (what they *say*, *think*, *feel*, and *do*)  
- **Context narrative** — a short story about how personas experience your domain  
- **Optional alignment table** linking persona motivations to affordances or API capabilities  

---

## 🧠 Coaching Sequence

### STEP 1 — Begin with Purpose  
> “Who are you designing *for*, and why does this matter?”

Describe the environment and human goals behind your system.

### STEP 2 — Identify Key Roles  
List the distinct user or participant types.  
Avoid job titles — use functional labels like “The Builder,” “The Maintainer,” etc.

### STEP 3 — Build Each Persona  
For each role, describe:  
- **Motivations**  
- **Frustrations**  
- **Skills & Tools**  
- **Desired Outcomes**

### STEP 4 — Map Experience  
Complete an **Empathy Map** for one or more personas: *Says / Thinks / Feels / Does.*

### STEP 5 — Write the Context Narrative  
> “How do these personas shape the world your system must live in?”  
Summarize their collective environment.

### STEP 6 — Reflect and Apply  
> “What design priorities change now that you understand these personas better?”  
Document the implications for design or policy.

---

## 🗂 Optional Reports & Deliverables

- Persona Summary Table  
- Empathy Map Diagram  
- Human Context Brief  
- Alignment Table (persona needs ↔ affordances)

---

## 💬 Explainer (for New Users)

A *persona* is a fictional but realistic character who represents one kind of person your system must serve.  
Ask: *Who are they? What do they need? What frustrates them?*  
No UX training required — just curiosity and empathy.

> The goal isn’t perfection. It’s **awareness** — of the humans your system will touch.

---

## ❓FAQ Addendum

**Do personas feed into other coaches?**  
Not directly. They inform better decisions later.

**How many personas?**  
Start small — two or three.

**What if I already have user stories?**  
Personas give those stories context.

**Do personas replace user research?**  
No — they complement it.

**How do I know they’re “right”?**  
They’re not about correctness — they’re about usefulness.

**What happens after this coach?**  
You move to *Domain Discovery* or *API Story* with clearer empathy.

---

## 📘 Example Session: Tool Shed Sharing Program  

This worked example demonstrates a full Persona Coaching session for a neighborhood tool-sharing system.

### Purpose Statement
> “This system helps neighbors borrow, lend, and track shared tools so that the community can make better use of what it already owns.”

### Personas

#### 1. Typical Neighbor  
- **Motivations:** Occasionally needs tools for immediate problems without buying them.  
- **Frustrations:** Tools missing, wrong selection, or misplaced.  
- **Skills & Tools:** Comfortable with phones/laptops; basic tool knowledge; uses YouTube for instruction.  
- **Desired Outcome:** Finds, uses, and returns the right tool easily.  
- **Empathy Map:**  
  - **SAYS:** “I just need this one tool for a quick fix.”  
  - **THINKS:** “I hope it’s actually there.”  
  - **FEELS:** Anxious at first, relieved afterward.  
  - **DOES:** Checks app, reserves, uses, returns on time.

#### 2. Tool Shed Supervisor  
- **Motivations:** Keep the system organized and trusted.  
- **Frustrations:** Missing tools or incomplete logs.  
- **Skills:** Proficient with admin tools; manages maintenance.  
- **Desired Outcome:** Accurate inventory and cooperative community.  
- **Empathy Map:**  
  - **SAYS:** “I just want to know what’s available and what needs fixing.”  
  - **THINKS:** “If I keep it simple, more people will use it.”  
  - **FEELS:** Pride when it runs smoothly; stress when it doesn’t.  
  - **DOES:** Reviews logs, sends reminders, coordinates repairs.

#### 3. New Neighbor  
- **Motivations:** Learn and feel included.  
- **Frustrations:** Unclear rules and fear of doing something wrong.  
- **Skills:** Basic phone user, limited tool familiarity.  
- **Desired Outcome:** Quick onboarding and confidence in borrowing.  
- **Empathy Map:**  
  - **SAYS:** “I don’t want to mess anything up.”  
  - **THINKS:** “Everyone else seems to know this.”  
  - **FEELS:** Nervous at first; proud after success.  
  - **DOES:** Reads help pages, asks questions, double-checks returns.

#### 4. Heavy User  
- **Motivations:** Frequent access to reliable tools for ongoing projects.  
- **Frustrations:** Delays, unavailable items, or disorganized shelves.  
- **Skills:** Advanced tool and app user.  
- **Desired Outcome:** Fast, consistent, reliable system; community recognition.  
- **Empathy Map:**  
  - **SAYS:** “I can’t start until that drill’s back.”  
  - **THINKS:** “This could run more efficiently.”  
  - **FEELS:** Frustration at downtime; satisfaction when system performs.  
  - **DOES:** Checks status often, mentors others, provides feedback.

---

### Context Narrative
In this neighborhood, tool sharing is both practical and social.  
The **Supervisor** ensures reliability; the **Typical Neighbor** represents normal use; the **New Neighbor** reflects accessibility; the **Heavy User** tests efficiency.  
Together they form a living ecosystem of trust and cooperation — the human baseline that shapes future design choices.

### Design Implications
- Improve discoverability and labeling.  
- Add tool condition indicators.  
- Provide onboarding guides for new users.  
- Notify supervisors about overdue tools.  
- Recognize heavy users’ contributions.

### Persona Summary Table
| Persona | Motivation | Frustration | Skill | Desired Outcome |
|----------|-------------|-------------|--------|----------------|
| Typical Neighbor | Borrow easily | Missing tools | Medium | Smooth cycle |
| Supervisor | Maintain system | Incomplete logs | High | Reliable flow |
| New Neighbor | Learn & belong | Unclear process | Low | Confidence |
| Heavy User | Frequent use | Delays & inefficiency | High | Reliability & recognition |

---

## 🧩 Next Steps
Use this example as a reference when running your own session.  
You can adapt its structure for any domain, substituting your own personas, empathy maps, and narratives.

---

## 📜 Footer & License

**Validation Summary:** PASS  
This document integrates the AI-Coaching Baseline v1.7 and Ethics Statement (2025-10-16)  
and conforms to the Classic Narrative-First Context Kit format.  

© 2025 Amundsen Consulting — Narrative-First AI-Coaching Framework  
Licensed CC BY-NC-SA 4.0

