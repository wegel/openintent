---
name: openintent-implement
description: Shape human-owned intent and compile it into features, fixes, refactors, migrations, protocol changes, formal verification, performance work, and user-experience changes in repositories that use OpenIntent. Use whenever an LLM reorganizes intent or changes software whose intent lives beside the code in prose, specifications, images, recordings, formal models, theorem statements, machine-checked proofs, measurements, examples, or other project sources.
---

# Implement from intent

## Read the project

Read `OPENINTENT.md` before changing product behavior, architecture, protocols, security, performance, or user experience. Follow the repository's agent instructions too.

Use the intent map to find the sources that govern the requested change. Read the user's request, the current behavior, the affected code, and the relevant tests, formal models, and checkers.

Treat chat, issues, and temporary working records as useful context unless `OPENINTENT.md` grants them control over lasting product choices. Move any lasting choice from those records into the mapped intent source.

## Carry the active work

Restate the purpose and keep a short native plan with concrete checks. Update that plan as work proceeds so the chat shows what is done, what changed, and what comes next. Track surprises, decisions, failed approaches, command results, and evidence when they will affect the rest of the work. Record a recovery path before any risky step could leave the project in a partial state.

Maintain the working state yourself. If the work cannot finish in the current chat or context may be lost before completion, leave the smallest self-contained temporary handoff that lets a fresh LLM resume from the repository alone. Include the purpose, current state, relevant discoveries and decisions not yet promoted elsewhere, unresolved human choices, checks and evidence, recovery information, and next steps. Keep it current without asking the human to edit it. Remove or squash it before merge unless the project deliberately keeps it.

## Show the human your read

After enough read-only inspection to identify the governing source, but before a new human request or correction causes any write, post this checkpoint visibly in the chat:

```text
My read

- <classification>: <precise interpretation>
- Governing source: <path and section, or "none mapped yet">
- This round: <intent, implementation, formal proof, experiment, or human choice you will work on>
```

Use these classifications:

- `Implementation defect`: the mapped source already says what the product should do.
- `Missing choice`: no mapped source answers a meaningful product or system question.
- `Changed choice`: the human now wants something different from the mapped source.
- `Intent refactor`: the sources need a better shape but the product should not change.
- `Exploration`: the human has not chosen yet and wants evidence from a prototype, test, measurement, or discussion.

Split a mixed request into separate classified bullets. Name exact paths and sections rather than claiming that "the spec" covers something. If later evidence changes your reading, post a revised `My read` block before continuing. Do not bury the checkpoint in a native plan or wait until after edits. The human must be able to correct your interpretation and notice when you stop following OpenIntent.

## Shape intent

Ask two separate questions: Does the mapped source already describe the desired product? Can a human find, understand, and change that idea without wading through unrelated material?

- If the source describes the product clearly, leave it alone. When the human asks you to compile, repair the code without adding text that merely restates a bug.
- If the source contains the right choices but hides them inside a giant file, scatters them across several files, or gives several sources overlapping control, refactor the intent before compiling. Preserve its meaning unless the human chooses to change it. Gather the choices around a durable idea that people will work on again, not around the current defect.
- If it does not, help the human write the lasting product truth. Describe the behavior people should keep, not the defect that exposed its absence.
- If the change requires a material product choice, show the choice and its consequences to the human before deciding for them, unless the mapped intent deliberately gives the LLM that choice.

When the human asks to shape, discuss, or reorganize intent, inspect code, tests, and current behavior as evidence, but do not edit implementation files. Wait until the human asks you to compile the current intent. The human may instead ask for a specific prototype or test when running something will teach them what they want.

The human and LLM may spend any number of rounds shaping intent before compiling it. They may return to intent when implementation teaches them something. Experiments do not become accepted intent merely because they run.

Use the medium that carries each choice best. A mockup can govern visual hierarchy, a recording can govern timing and feel, a formal model can govern a protocol invariant, and a benchmark target can govern speed. Use prose to connect these sources, not to flatten all of them into text.

Write for a creative peer. Prefer vivid product language such as "Play picks up where you left off" over legal clauses, exhaustive state tables, or text shaped around one bug. Present the product as it should now exist for a reader who never saw the design conversation. Mention an earlier alternative only when its consequences still constrain future work. Put machine-useful expansions in tests or generated views unless they reveal a choice the human should own.

## Preserve formal claims

When a project uses formal methods, use `OPENINTENT.md` to distinguish the definitions, model rules, theorem statements, assumptions, proof code, and generated results by the role each one plays. A map may point to exact declarations or regions when one file mixes human-owned intent with work left to the LLM.

Treat a change to a mapped claim, its assumptions, or the behavior it promises to cover as intent work. Show that change in `My read` and shape it with the human unless the mapped intent delegates the choice. Never make a checker pass by quietly weakening a claim, adding an unaccepted assumption or unfinished proof placeholder, narrowing the covered cases, or disconnecting the checked model from the implementation.

During a compile, create or repair the proof as implementation work. Run the repository's configured checker. Report the exact claims it accepted, their assumptions, the code or protocol tied to them, and the important code or interfaces it did not examine. A machine-checked proof establishes its stated claim, not that the claim expresses what the human wants.

## Compile and learn

Once the human asks you to compile, work on a normal branch with the repository's normal tools. Implement the mapped intent and test the real behavior.

When the human reports a bug, bad behavior, or poor experience, keep it in the current compile loop. Compare the desired result with the mapped source before deciding what to edit:

- If the source already gives a clear answer, repair the code and strengthen the test, benchmark, model, recording, device check, or machine-checked proof that supplies evidence for it. Do not add prose that restates the defect.
- If the source leaves a meaningful product or system choice open, explain that choice and its consequences, shape it with the human, and then continue compiling.
- If using the product changes what the human wants, revise the controlling source and compile the new intent.
- If the source contains the right answer but makes people hunt for it, refactor the source without pretending that the product changed.

Do not start a separate workflow merely because the LLM introduced the defect or the human used the word "fix." Keep replaceable mechanisms such as locks, cache structures, retry plumbing, and file names in code, tests, or durable engineering notes unless a human needs to control them directly.

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
- Run the repository's normal tests, visual checks, benchmarks, simulations, device runs, and configured formal checkers.
- Give the human enough direct evidence to judge the parts that automated checks cannot settle.
- Report which intent sources you used, which ones changed, what the code now does, what evidence you gathered, and which questions remain. When formal proof applies, include its exact claims, assumptions, connection to the realized software, and unchecked edges.

Do not claim that passing tests prove every reasonable reading of the intent or that a checked theorem covers behavior outside its stated claim and linked software. The human still decides whether the result is the product they want.
