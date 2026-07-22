# OpenIntent workflow

This repository uses OpenIntent. Read `OPENINTENT.md` before changing product behavior, architecture, protocols, security, performance, or user experience.

When the skills are available:

- Use `$openintent-implement` to change intent and code.
- Use `$openintent-review` in a separate, read-only review of the finished branch.

If mapped intent already describes the requested result, repair the code without adding text that merely restates the bug. If the request needs a new lasting product choice, ask the human when needed and update the source that controls it. Write for a reader who did not see the chat, and mention an earlier alternative only when its consequences still matter. Keep intent pleasant to read and use visual, interactive, formal, or measured sources when they communicate better than prose.

When a formal source controls a choice, use `OPENINTENT.md` to distinguish its human-owned claims, assumptions, and proof choices from work left to the LLM. Do not make a checker pass by quietly weakening a claim, adding an unaccepted assumption or unfinished placeholder, narrowing what it covers, or disconnecting the checked model from the realized software. Run the configured checker and tell the human exactly what it established and what it did not examine.

When the human asks to shape or reorganize intent, inspect code, tests, and current behavior as evidence, but do not change implementation files until the human asks you to compile the current intent or build a specific experiment. Refactor an intent source when readers must hunt through a giant file, several overlapping files, or unrelated details to understand one product idea. Preserve the product's meaning unless the human chooses to change it. Organize sources around durable ideas that humans work on, not around individual prompts or defects.

When the human reports a bug, bad behavior, or poor experience during compiling, keep it in the same work loop and compare it with the mapped source. Repair code and strengthen tests when the source already gives a clear answer. Return to shaping when the source leaves a meaningful choice open, when real use changes what the human wants, or when the source itself needs refactoring. Keep replaceable mechanisms such as locks, cache structures, retry plumbing, and file names out of human-owned intent unless the human needs to control them directly.

After enough read-only inspection to ground your answer, but before every new request or correction causes a write, post this visible checkpoint in the chat:

```text
My read

- <classification>: <precise interpretation>
- Governing source: <path and section, or "none mapped yet">
- This round: <intent, implementation, formal proof, experiment, or human choice you will work on>
```

Use `Implementation defect`, `Missing choice`, `Changed choice`, `Intent refactor`, or `Exploration`. Split mixed requests into separate classified bullets. If evidence changes your reading, post a revised `My read` block before continuing. Do not hide this checkpoint inside a plan or wait until after the edits. Its absence should be visible to the human.

Keep the active purpose, plan, progress, discoveries, decisions, checks, and evidence in the chat and native agent plan. Maintain that working state yourself. If work must cross a chat boundary, leave the smallest self-contained temporary handoff that lets a fresh LLM resume from the repository alone. Maintain it yourself, then remove or squash it before merge unless the project wants to keep it.

Follow this repository's normal branch, test, CI, and human-approval rules. Before handoff, state:

- which intent sources governed the change;
- which intent sources changed;
- what the code now does;
- which tests, images, recordings, benchmarks, simulations, device runs, or machine-checked proofs support it;
- which questions still need human judgment.
