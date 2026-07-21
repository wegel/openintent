---
name: openintent-implement
description: Implement features, fixes, refactors, migrations, protocol changes, performance work, and user-experience changes in repositories that use OpenIntent. Use whenever an LLM changes software whose human-owned intent lives beside the code in prose, specifications, images, recordings, formal models, measurements, examples, or other project sources.
---

# Implement from intent

## Read the project

Read `OPENINTENT.md` before changing product behavior, architecture, protocols, security, performance, or user experience. Follow the repository's agent instructions too.

Use the intent map to find the sources that govern the requested change. Read the user's request, the current behavior, the affected code, and the relevant tests or proof tools.

Treat chat, issues, and temporary working records as useful context unless `OPENINTENT.md` grants them control over lasting product choices. Move any lasting choice from those records into the mapped intent source.

## Carry the active work

Restate the purpose and keep a short native plan with concrete checks. Update that plan as work proceeds so the chat shows what is done, what changed, and what comes next. Track surprises, decisions, failed approaches, command results, and evidence when they will affect the rest of the work. Record a recovery path before any risky step could leave the project in a partial state.

Maintain the working state yourself. If the work cannot finish in the current chat or context may be lost before completion, leave the smallest self-contained temporary handoff that lets a fresh LLM resume from the repository alone. Include the purpose, current state, relevant discoveries and decisions not yet promoted elsewhere, unresolved human choices, checks and evidence, recovery information, and next steps. Keep it current without asking the human to edit it. Remove or squash it before merge unless the project deliberately keeps it.

## Shape the change

Decide whether the existing intent already describes the desired result.

- If it does, repair the code. Do not add cosmetic intent text that merely restates a bug.
- If it does not, help the human write the lasting product truth. Describe the behavior people should keep, not the defect that exposed its absence.
- If the change requires a material product choice, show the choice and its consequences to the human before deciding for them, unless the mapped intent deliberately gives the LLM that choice.

Prefer clear intent before implementation when that helps the human steer the work. The human and LLM may also test code or prototypes to learn what feels right. Such experiments do not become accepted intent merely because they run.

Use the medium that carries each choice best. A mockup can govern visual hierarchy, a recording can govern timing and feel, a formal model can govern a protocol invariant, and a benchmark target can govern speed. Use prose to connect these sources, not to flatten all of them into text.

Write for a creative peer. Prefer vivid product language such as "Play picks up where you left off" over legal clauses, exhaustive state tables, or text shaped around one bug. Present the product as it should now exist for a reader who never saw the design conversation. Mention an earlier alternative only when its consequences still constrain future work. Put machine-useful expansions in tests or generated views unless they reveal a choice the human should own.

## Implement and learn

Work on a normal branch with the repository's normal tools. Implement the mapped intent and test the real behavior.

When code, tests, devices, or users reveal a missing choice:

1. Explain the discovery in plain language.
2. Ask the human when the choice would change the product in a meaningful way.
3. Update the source that controls that choice after the human decides.
4. Continue from the revised intent.

Keep code-level facts in code, tests, or the repository's durable engineering notes. Do not force every implementation detail into human-owned intent.

## Finish coherently

Before handing the change back:

- Compare the final code diff with the final relevant intent, not only with the original request.
- Put every lasting product choice discovered during the work into the source that controls it.
- Run the repository's normal tests, visual checks, benchmarks, simulations, or device proof.
- Give the human enough direct evidence to judge the parts that automated checks cannot settle.
- Report which intent sources you used, which ones changed, what the code now does, what evidence you gathered, and which questions remain.

Do not claim that passing tests prove every reasonable reading of the intent. The human still decides whether the result is the product they want.
