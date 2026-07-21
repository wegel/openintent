---
name: openintent-review
description: Review a branch, pull request, patch, implementation, or release candidate against the human-owned intent in an OpenIntent repository. Use for an independent read-only review of product behavior, protocols, architecture, security, performance, UI and UX, tests, visual evidence, or other claims before a human approves upstream changes.
---

# Review code against intent

Review from the repository, not from the implementation chat's memory. Do not modify the branch under review.

## Reconstruct the intended result

Read `OPENINTENT.md`, the base-to-head diff, every mapped source that governs the changed choices, and the repository's agent instructions. Read relevant issues and temporary working records for context, but do not treat them as lasting intent unless the map says they control a choice.

For each changed product choice, identify the source that controls it. Do not demand an intent edit when an existing source already covers the result or deliberately delegates the choice to the LLM. Do report any other lasting choice that appears only in code, chat, an issue, or a temporary working record.

## Challenge the result

Check whether the branch:

- contradicts, narrows, or silently expands the mapped intent;
- matches the final intent after discoveries changed it during implementation;
- proves its important claims with the repository's normal tests, visual checks, benchmarks, simulations, recordings, or device runs;
- preserves shared behavior across apps, roles, and protocol participants where the intent requires it;
- hides a product choice inside code or a test fixture;
- carries design-conversation history into intent when no current choice depends on it;
- presents uncertain or subjective evidence as settled fact.

Run or inspect the normal checks that fit the risk. Judge images, recordings, prototypes, measurements, and formal models directly when they control the relevant choice. Do not ask prose to stand in for them.

## Report to the human

List blockers first, then open product questions, then conclusions that the evidence supports. Name the exact intent source, code path, and proof behind each important finding.

End with one verdict:

- `Ready for human review`
- `Needs human decision`
- `Needs work`

CI checks deterministic facts. This review catches mismatches and missing choices. A human still decides whether to approve the branch upstream.
