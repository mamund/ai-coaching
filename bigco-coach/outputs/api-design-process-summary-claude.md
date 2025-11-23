**Session Summary**

You came in with a specific concern: you lack confidence that your API design process produces the "right" API. Important details get missed over the design and build cycle, and by the time you deliver, the result doesn't match what was actually needed.

We explored this through two historical lenses from the BigCo framework:

**Leona Woods (measurement and instrumentation)** helped frame the core problem. Your existing process had a checkpoint—showing the design to the requesting team and getting approval—but that instrument wasn't measuring what you needed. A "looks fine" approval didn't carry real signal about alignment. The requesting team's understanding was still evolving, and you had no way to detect drift between their approval and their eventual clarity.

**Frederick Jones (practical engineering and iteration)** added the insight that you were testing the blueprint, not the thing in motion. He emphasized finding the cheapest way to be wrong—getting something concrete in front of consumers early, before you've invested in full implementation.

**What we built:**

A staged process that moves from cheap to expensive, with active work replacing passive approval:

1. **Paper prototype stage.** Both sides write independent narratives—consumer describes what they need, server team describes what they intend to provide. You compare these documents and record matches, gaps, conflicts, and open questions.

2. **Contract mock stage.** Once paper alignment is achieved, you stand up a mock API. The consumer writes integration code against it. Their working client code becomes evidence of real alignment.

3. **Implementation.** Only after both stages confirm alignment do you build the real thing.

**Key shifts:**

- From asking "is this fine?" to comparing two independent artifacts
- From passive review to active work (they write the narrative, they write the client code)
- From a single late checkpoint to staged investment with early, cheap feedback

You now have a documented process with templates you can adapt as you learn what works in your environment.
