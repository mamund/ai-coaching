# API Design Alignment Process

## Purpose

This process reduces the gap between what consumers need and what gets built. It creates two independent artifacts—one from the consumer, one from the server team—and uses their comparison to surface misalignment before implementation begins.

## Principles

**Passive approval is unreliable.** When someone reviews a spec and says "looks fine," they're pattern-matching against an incomplete mental model. Their "yes" means "I don't see an obvious problem," not "this will meet my needs."

**Active work reveals understanding.** Asking consumers to write their own narrative—and later, their own integration code—forces them to articulate what they actually need. Gaps in their thinking become visible.

**Comparison beats review.** Instead of asking "is this right?", compare two independent documents. Misalignment shows up in the differences.

**Stage your investment.** Move from cheap to expensive: paper first, then contract mock, then implementation. Catch problems when they cost the least to fix.

## Process Stages

1. **Paper prototype.** Consumer and server team each write a short narrative describing the interaction.
2. **Alignment review.** Compare the two narratives. Document matches, gaps, conflicts, and open questions.
3. **Resolve differences.** Rework until no unresolved conflicts remain.
4. **Contract mock.** Define the API contract and stand up a mock server. Consumer writes integration code against it.
5. **Validate integration.** Consumer's working client code confirms alignment. Resolve any new issues.
6. **Implementation.** Build the real API. Risk of misalignment is now low.

## Consumer Narrative Template

The requesting team completes this for each interaction or flow.

1. **What triggers this call and what do you need back?** Describe the situation or event in your system that initiates the request, and what response you expect.

2. **What will you do with the response?** Explain how you will use each piece of data returned.

3. **What could go wrong that you'd need to handle?** Describe failure scenarios and how you would respond to them.

## Server Endpoint Template

The server team completes this independently, before seeing the consumer narrative.

1. **What triggers this call and what does it return?** Describe the expected use case and the response structure.

2. **What inputs are required, optional, or conditional?** List the parameters and their constraints.

3. **What failure modes exist and how are they signaled?** Describe error conditions and their representations.

## Alignment Notes Template

After both narratives are complete, compare them and record:

1. **Matches.** Where consumer and server descriptions agree.
2. **Gaps.** What one side expects that the other didn't mention.
3. **Conflicts.** Where both sides have expectations that contradict.
4. **Open questions.** Ambiguities that neither document resolves.

## The Matching Process

When comparing the two narratives, look for:

- **Mismatched expectations:** They expect data you weren't planning to return, or vice versa.
- **Naming or structure gaps:** They describe the inputs one way, you describe them another.
- **Unhandled failures:** They haven't considered a failure you know will happen, or they expect error information you weren't planning to surface.

Proceed to the contract mock stage only when alignment notes show no unresolved conflicts.

## Contract Mock Stage

Once paper alignment is achieved:

The server team defines the API contract (endpoints, request/response shapes, error cases) and stands up a mock server that returns plausible responses.

The consumer team writes a simple set of calls that exercise the mock and verifies the responses match their expectations.

Their working client code becomes evidence of alignment. If the contract doesn't fit their actual integration context, they'll discover it while writing the code—not after the real thing is built.

## Continuous Improvement

Track whether the same kinds of gaps recur across projects. If you consistently find misalignment in failure handling, or in optional inputs, that tells you where your templates or process need to be sharper.

---

*Developed using BigCo Coach v1.0*
