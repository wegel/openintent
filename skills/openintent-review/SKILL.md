---
name: openintent-review
description: Review an intent refactor, branch, pull request, patch, implementation, or release candidate against the human-owned intent in an OpenIntent repository. Use for an independent read-only review of source organization, product behavior, protocols, architecture, security, performance, UI and UX, formal models and proofs, tests, visual evidence, or other claims before a human approves upstream changes.
---

# Review code against intent

Review from the repository, not from the implementation chat's memory. Do not modify the branch under review.

## Reconstruct the intended result

Read `OPENINTENT.md`, the base-to-head diff, every mapped source that governs the changed choices, and the repository's agent instructions. Read relevant issues and temporary working records for context, but do not treat them as lasting intent unless the map says they control a choice.

For each changed product choice, identify the source that controls it. Do not demand an intent edit when an existing source already covers the result or deliberately delegates the choice to the LLM. Do report any other lasting choice that appears only in code, chat, an issue, or a temporary working record.

If the branch only refactors intent, compare the old and new sources. Check that the new path preserves every existing choice unless the diff clearly makes a deliberate product change. A fresh reader should be able to find the new source from `OPENINTENT.md`, understand what it controls, and tell which older source no longer controls that area. Do not demand implementation work when the human has not asked to compile yet.

When formal sources apply, determine which definitions, model rules, theorem statements, assumptions, and proof code carry human choices and which parts the LLM owns. Use exact declarations or regions when a file mixes both roles.

## Challenge the result

Check whether the branch:

- contradicts, narrows, or silently expands the mapped intent;
- matches the final intent after discoveries changed it during implementation;
- supports its important claims with the repository's normal tests, visual checks, benchmarks, simulations, recordings, or device runs;
- preserves shared behavior across apps, roles, and protocol participants where the intent requires it;
- hides a product choice inside code or a test fixture;
- leaves duplicate or unclear authority after moving an idea between intent sources;
- weakens a mapped formal claim, adds an assumption, or narrows its covered cases without showing the human an intent change;
- leaves an unfinished proof placeholder or claims more than the checker established;
- claims that a checked model covers realized software without showing how the two connect;
- carries design-conversation history into intent when no current choice depends on it;
- presents uncertain or subjective evidence as settled fact.

Run or inspect the normal checks that fit the risk. Judge images, recordings, prototypes, measurements, and formal models directly when they control the relevant choice. When formal proof supports a claim, run the configured checker, inspect its assumptions and unfinished placeholders, and identify the exact claim and realized code or protocol it covers. Do not ask prose to stand in for rich sources or infer correctness merely because a proof file exists.

## Report to the human

List blockers first, then open product questions, then conclusions that the evidence supports. Name the exact intent source, code path, and evidence behind each important finding. For a formal result, name the checked claim, its assumptions, its connection to the realized software, and the important parts the checker did not examine.

End with one verdict:

- `Ready for human review`
- `Needs human decision`
- `Needs work`

CI checks deterministic facts, including formal claims when the project configures a checker. This review catches mismatches, weakened claims, and missing choices. A human still decides whether to approve the branch upstream.
