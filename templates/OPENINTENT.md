# Project intent map

This repository keeps human-owned intent beside the code. Git records each draft and accepted change. LLMs implement and review that intent on normal branches. CI checks deterministic facts, and a human approves upstream changes.

## Sources and the choices they control

Replace these examples with the real paths in this repository. Add a row for every source that controls product behavior. One source may control several areas, and one area may use several media.

| Product or code area | Human-owned source | Choices this source controls | Useful evidence or check |
| --- | --- | --- | --- |
| Example protocol | `specs/protocol.md` and `models/protocol.tla` | Messages, participant duties, failure rules, and safety invariants | Model checks, compatibility tests, and fault simulation |
| Example mobile UI | `specs/mobile.md` and `design/mobile/` | User flow, visual hierarchy, interaction feel, and accessibility | Device tests, screenshots, recordings, and human use |
| Example service | `specs/service.md` | Service behavior, limits, security boundaries, and performance targets | Unit and integration tests, threat tests, and benchmarks |

Say which source controls a choice when several sources overlap. If two sources disagree, a human resolves the product choice and updates the sources or this map. Current code, another app, or a prototype counts as evidence unless this map explicitly grants it control over a choice.

A formal artifact can carry intent, supply evidence, or do both. A formal file may mix human-owned definitions, model rules, theorem statements, assumptions, or proof choices with work left to the LLM. Map exact declarations or regions when the whole file does not carry the same authority. Name the repository command that checks them and the realized code or protocol they cover. A passing checker establishes only the mapped claim, not behavior in code or interfaces it did not examine.

Changing a mapped formal claim, its assumptions, or the behavior it promises to cover changes intent. Repairing its proof normally does not. Do not let an LLM weaken the claim, add an unaccepted assumption or unfinished placeholder, narrow the covered cases, or disconnect the model from the realized software merely to make a checker pass.

Within each source, authors may mark a choice as required, directional, exemplary, open for exploration, delegated to the LLM, or reserved for a human. Use the project's natural language and structure. Do not turn these meanings into a form that authors must fill out for every idea.

## How changes move

- Read the mapped sources before changing product behavior, architecture, protocols, security, performance, or user experience.
- After enough read-only inspection to identify the governing source, show the human a `My read` checkpoint before editing. Classify the request as an implementation defect, missing choice, changed choice, intent refactor, exploration, or a mixture; name the source and say what this round will edit. Post a revised checkpoint before continuing if later evidence changes that reading.
- If the existing intent already describes the desired result, repair the code without adding bug-shaped prose.
- If the existing intent hides a coherent idea inside a giant source or scatters it across several sources, refactor those sources before compiling. Preserve their meaning unless the human chooses to change it, and leave one clear authority for each choice.
- If the intent lacks a lasting product choice, write that choice in the source best suited to carry it.
- Write the product as it should now exist for a reader who never saw the design conversation. Include an earlier alternative only when its consequences still constrain future work.
- Let the human and LLM shape intent for as many rounds as useful. During those rounds, inspect the implementation as evidence but change it only when the human asks to compile the current intent or build a specific experiment.
- Use code and prototypes to learn when needed. Once the human asks to compile, implementation and tests may expose choices that send the work back to intent.
- Keep bugs and disappointing behavior inside the current compile loop. Compare each reported problem with the mapped source instead of automatically editing intent or automatically leaving it unchanged.
- When the source already answers the question, repair the implementation and strengthen its evidence. When the source is silent, real use changes the desired product, or the source proves hard to use, return to shaping before continuing.
- Keep replaceable code mechanisms in code, tests, or durable engineering notes unless a human needs to control them directly.
- When a formal source governs a choice, preserve its mapped claims and assumptions while compiling. Run its checker and report the exact accepted claims, their assumptions, the software tied to them, and the important parts the checker did not examine.
- When implementation or tests expose a missing choice, bring it to the human and revise the mapped source.
- Before review, reconcile the finished code with the finished intent.

## Active work

The implementation LLM keeps its purpose, plan, progress, discoveries, decisions, checks, and evidence in the active chat and native plan. The LLM maintains this working state while the human steers the product.

Issues, chat transcripts, and temporary working records provide context unless the table above says they control a lasting choice. Move lasting choices into the mapped source before review. If work crosses a chat boundary, the LLM leaves the smallest self-contained temporary handoff that lets a fresh LLM resume from the repository alone. The LLM maintains it and removes or squashes it before merge.

## Human judgment

Automated checks cannot decide whether every visual, interaction, tradeoff, or product choice feels right. Each pull request must show the human the evidence they need to judge those parts directly.
