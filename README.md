# AI coaching for API design

## overview

This repository hosts a growing collection of AI coaches. Each coach is an interactive, in chat assistant that helps developers, designers, and architects think more clearly about API design using narrative first reasoning, structured exploration, and affordance aware techniques.

Every coach is a context kit. It is a self contained Markdown file that you can load into any modern LLM. Once loaded, the coach guides you through a deliberate workflow that turns early ideas into well formed API artifacts.

The coaches follow the AI guided reasoning and exploration framework. They are built to support human decision making, not automate it. The tools help you find intention, surface constraints, and shape structure while keeping you in control of the design process.

**NOTE** 
> This is all very much a "work in progress." Expect things to change, bugs, and surprises. If you are trying thes out, I'd love to hear from you on what worked, what didn't and how I can improve things.  Fee free to leave an issue w/ details on contact me online. -- *MikeA*
---

## why ai coaching

Most tools assume you already know what your API should look like. These coaches help you discover, not merely document. They offer structure when you need it and give you room to think when the path forward is still forming.

The coaches:

* support a narrative first approach to design
* guide you through an intentional workflow
* help you articulate purpose, resources, and actions
* produce artifacts ready for downstream formats
* preserve human judgment while speeding up mechanical steps

The result is a design process that feels more like good teaching and less like wrestling with templates.

---

## how it works

Each coach includes:

1. **a context kit** that sets up operating rules, workflow, tone, and safety
2. **a guided session pattern** that keeps the conversation structured
3. **consistent deliverables** such as API Stories, ALPS profiles, and schemas

You load the context kit into an LLM of your choice. The coach then runs the session start behavior, asks you to confirm the workflow, and proceeds step by step.

This approach provides a stable teaching experience across ChatGPT, Claude, Gemini, and other models.

---

## available v2.0 coaches

The following coaches have been released for the v2.0 framework. Each one includes full session start behavior, runtime behavior rules, and cross model safeguards.

### API story coach v2.0

Helps you create a clear, structured API Story that becomes the foundation for ALPS, OpenAPI, and other formats. Includes the classic output style and the Task Management example.

### thinking with machines coach v2.0

Introduces the historical and conceptual grounding of augmentation, symbiosis, and the lineage that runs from Bush to Licklider to Engelbart. Helps learners understand how to work with AI tools as partners in reasoning.

### vocabulary coach v2.0

Guides you through identifying, naming, and aligning vocabulary items used in your domain. Helps you create consistent property names and semantic groupings that carry across your API design.

### persona coach v2.0

Helps you develop user personas that shape narrative based API design. Supports exploration of roles, goals, constraints, and motivations.

More coaches are on the way, including ALPS, AsyncAPI, OKR and KPI, Composable Service Design, and Change Management.

---

## requirements

* any modern AI chat interface such as ChatGPT, Claude, or Gemini
* no installation or code setup required
* optional: Node.js if you want to run any future out of chat utilities

---

## responsible use

AI coaches run inside public LLM platforms. Do not include personal, private, or company confidential data in your sessions.

The tools in this repository are designed for education, exploration, and structured reasoning. They are not intended for production operations or decision making without human review.

For more, see the ethics and safety section in this repository.

---

## getting started

1. Open the AI platform of your choice
2. Copy the content of a coach’s Markdown file into a new chat
3. Use the BEGIN phrase listed at the top of the kit
4. Follow the structured workflow

Example:

```
BEGIN: API Story Coaching Session
```

The coach will take you through each step at a manageable pace and help you produce a complete, validated artifact.

*NOTE*
> Each coach is designed to operate as a stand-alone element. You do not need to load any other context data to start a coaching session. In some cases, the coach might give yuou the opportunity to share input data (an ALPS profile document, a list of vocabulary words, etc.). As usual, be careful on what you share with a pulbic LLM.
> 
