# OpenIntent workflow

This repository uses OpenIntent. Read `OPENINTENT.md` before changing product behavior, architecture, protocols, security, performance, or user experience.

When the skills are available:

- Use `$openintent-implement` to change intent and code.
- Use `$openintent-review` in a separate, read-only review of the finished branch.

If mapped intent already describes the requested result, repair the code without adding text that merely restates the bug. If the request needs a new lasting product choice, ask the human when needed and update the source that controls it. Write for a reader who did not see the chat, and mention an earlier alternative only when its consequences still matter. Keep intent pleasant to read and use visual, interactive, formal, or measured sources when they communicate better than prose.

Keep the active purpose, plan, progress, discoveries, decisions, checks, and evidence in the chat and native agent plan. Maintain that working state yourself. If work must cross a chat boundary, leave the smallest self-contained temporary handoff that lets a fresh LLM resume from the repository alone. Maintain it yourself, then remove or squash it before merge unless the project wants to keep it.

Follow this repository's normal branch, test, CI, and human-approval rules. Before handoff, state:

- which intent sources governed the change;
- which intent sources changed;
- what the code now does;
- which tests, images, recordings, benchmarks, simulations, or device runs support it;
- which questions still need human judgment.
