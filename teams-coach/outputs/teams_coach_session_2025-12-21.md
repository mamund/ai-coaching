# Teams Coach Session Artifact

**Session Date:** December 21, 2025  
**Work Examined:** Adding two UI fields to an app display  
**Coach:** Teams Coach v1.0

---

## Traced Work Summary

**Initial expectation:** Solo UI work  
**Actual involvement:** Six groups (Team lead, UI, Services team, Documentation team, QA, Operations)

### Handoff Sequence

The work moved through nine formal handoffs:

1. Team lead → informal request → you
2. You → formal change order → services team
3. Services team → approval → you
4. You → final update → team lead
5. Team lead → approval → you
6. You → code → QA
7. You → change order → docs team (parallel with coding)
8. QA → approved code → operations
9. Docs team → documentation → operations (for release)

**Informal coordination:** Multiple Slack messages, hallway conversations, and emails occurred throughout change order writing and coding phases. QA and operations had additional ad-hoc follow-up questions.

---

## Coordination Observations

### Built-in Pause Points

Five structural stops exist in the workflow, primarily driven by scheduling pressure:

- Services team → approval → back to you
- Team lead → approval → you
- You → change order → docs team (parallel with coding)
- QA → approved code → operations
- Docs team → documentation → operations (for release)

### Slowest Decision

**Team lead's final change order approval** (before coding could begin)

**Cause:** Not disagreement or complexity—capacity constraints. The team lead manages multiple competing priorities.

### Heaviest Coordination

**Services team feedback loop**

- Consistently delayed
- Requires extensive informal back-and-forth communication
- Occurs even for small changes like adding two fields

### Smooth Flow Areas

- Direct collaboration between you and team lead works well
- Change order writing flows smoothly (single person)
- Coding proceeds without friction (single person)
- Operations release executes well once scheduled

---

## System Synthesis

**Of the nine handoffs, five happen before any code is written.**

Wait time and handoff delays consume the majority of cycle time before planned implementation work begins. This pattern repeats across all change orders, not just this specific two-field addition.

The system functions as a coordination-heavy workflow where alignment requirements significantly outweigh execution complexity, even for technically simple changes.

---

## Candidate Experiment

### Proposed Change

Send the change order draft to QA in parallel with the services team review, rather than sequentially after coding is complete.

### Mechanism

When you send the change order to services for feedback, simultaneously send the same draft to QA for their review. While services team reviews and provides feedback, QA can begin writing test plans in preparation for initial deployment.

### Expected Effects

- **Reduce sequential delays** by parallelizing work without hard dependencies
- **Surface QA questions earlier** when they might inform services review or vice versa
- **Utilize wait time** productively while services approval is pending

### Reversibility

If the change creates confusion, coordination overhead, or slows approvals, simply revert to the current sequential process. No structural damage occurs.

### Testing Approach

Try this experiment on the next small UI change (similar scope to the two-field addition) to contain risk and gather clear signal.

---

## Validation Check

✓ **Coordination cost accounted for:** Five pre-implementation handoffs identified and mapped; informal communication load recognized

✓ **Cognitive limits respected:** Team lead delay attributed to capacity constraints rather than motivation; services scheduling pressure acknowledged as structural

✓ **Proposed change is reversible:** Parallel handoff experiment is small, testable within 1-2 work cycles, and easy to undo

---

## Key Insight

The technical work (adding two fields to a UI) represents a small fraction of the total effort. The system's defining characteristic is coordination weight: formal handoffs, approval pauses, and informal alignment conversations that precede and surround implementation.

Understanding this pattern allows informed choices about where to invest improvement effort—not in speeding up coding, but in examining coordination structure itself.

---

## Next Steps (Optional)

- Run this coach again on a different piece of work to compare patterns
- Test the parallel QA experiment and observe results
- Notice whether the five-handoff-before-coding pattern appears consistently

---

**Session completed:** December 21, 2025  
**Context Kit:** Teams Coach Context Kit v1.0  
**License:** CC BY-NC-SA 4.0  
© 2025 amundsen.com, Inc.
