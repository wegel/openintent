# Project intent map

This repository keeps human-owned intent beside the code. Git records each draft and accepted change. LLMs implement and review that intent on normal branches. CI checks deterministic facts, and a human approves upstream changes.

## Sources and the choices they control

Replace these examples with the real paths in this repository. Add a row for every source that controls product behavior. One source may control several areas, and one area may use several media.

| Product or code area | Human-owned source | Choices this source controls | Useful proof |
| --- | --- | --- | --- |
| Example protocol | `specs/protocol.md` and `models/protocol.tla` | Messages, participant duties, failure rules, and safety invariants | Model checks, compatibility tests, and fault simulation |
| Example mobile UI | `specs/mobile.md` and `design/mobile/` | User flow, visual hierarchy, interaction feel, and accessibility | Device tests, screenshots, recordings, and human use |
| Example service | `specs/service.md` | Service behavior, limits, security boundaries, and performance targets | Unit and integration tests, threat tests, and benchmarks |

Say which source controls a choice when several sources overlap. If two sources disagree, a human resolves the product choice and updates the sources or this map. Current code, another app, or a prototype counts as evidence unless this map explicitly grants it control over a choice.

Within each source, authors may mark a choice as required, directional, exemplary, open for exploration, delegated to the LLM, or reserved for a human. Use the project's natural language and structure. Do not turn these meanings into a form that authors must fill out for every idea.

## How changes move

- Read the mapped sources before changing product behavior, architecture, protocols, security, performance, or user experience.
- If the existing intent already describes the desired result, repair the code without adding bug-shaped prose.
- If the intent lacks a lasting product choice, write that choice in the source best suited to carry it.
- Write the product as it should now exist for a reader who never saw the design conversation. Include an earlier alternative only when its consequences still constrain future work.
- Prefer clear intent before implementation when it helps the human steer. Use code and prototypes to learn when needed.
- When implementation or tests expose a missing choice, bring it to the human and revise the mapped source.
- Before review, reconcile the finished code with the finished intent.

## Active work

The implementation LLM keeps its purpose, plan, progress, discoveries, decisions, checks, and evidence in the active chat and native plan. The LLM maintains this working state while the human steers the product.

Issues, chat transcripts, and temporary working records provide context unless the table above says they control a lasting choice. Move lasting choices into the mapped source before review. If work crosses a chat boundary, the LLM leaves the smallest self-contained temporary handoff that lets a fresh LLM resume from the repository alone. The LLM maintains it and removes or squashes it before merge.

## Human judgment

Automated checks cannot decide whether every visual, interaction, tradeoff, or product choice feels right. Each pull request must show the human the evidence they need to judge those parts directly.
