# OpenIntent

OpenIntent treats human-owned intent as source and LLM-written code as a replaceable result of that source.

Version 0.1 uses repository files, ordinary Git branches, two LLM skills, normal CI, and human approval.

## How a project uses it

1. Keep intent beside the code in the same repository. Intent may live in prose, images, recordings, prototypes, formal models, measurements, examples, or any other useful medium.
2. Add an `OPENINTENT.md` map. The map tells humans and LLMs which sources control each product choice and which evidence can test it.
3. Wire the workflow into `AGENTS.md` or the repository's equivalent instructions.
4. Let the human and an LLM shape intent for as many rounds as useful. The LLM may inspect code and evidence, but it does not change the implementation until the human asks it to compile the current intent or to build a specific experiment.
5. Let an implementation LLM compile the current intent on a normal branch. It keeps the active plan and progress in the chat, revises intent when the work uncovers missing choices, and implements the revised intent.
6. Let a separate LLM review the finished branch against the finished intent.
7. Let normal CI run the project's deterministic checks, including any mapped model or proof checker, and let a human approve the branch upstream.

Git keeps drafts, branches, commits, rebases, squashes, temporary handoffs, and failed experiments. Each project decides what deserves a lasting place.

Shaping intent includes refactoring its sources. A human and LLM may split a giant specification, gather scattered choices, improve the path through several media, or rename concepts without changing what the product should do. This work matters even when the current code already violates a clearly written rule. OpenIntent does not require one source per request or one permanent record per discarded draft.

Problems found while compiling stay in the same loop. The LLM compares the desired result with the mapped source instead of assuming that every bug needs an intent edit or that no bug does. If the source already says what should happen, the LLM repairs the code and strengthens the evidence. If the source leaves a product choice open, the human and LLM shape that choice before continuing. If using the product changes the human's mind, they revise the intent. Code mechanisms remain in code, tests, and durable engineering notes unless a human needs to control them directly.

Before it edits intent or implementation for each new request or correction, the LLM shows the human how it read the change. A short `My read` block names the applicable classification, the governing source, and what the LLM will edit in the current round. The LLM uses `Implementation defect`, `Missing choice`, `Changed choice`, `Intent refactor`, or `Exploration`, and splits a mixed request when several apply. If later evidence changes that reading, the LLM posts a revised block before continuing. This visible checkpoint lets the human correct a misunderstanding and notice when an LLM has drifted from the OpenIntent workflow.

## Use formal proof where it fits

Some product choices can live in formal definitions, model rules, theorem statements, and explicit assumptions. A project may map those exact declarations as human-owned intent and usually let LLMs write the proof code and the implementation. When one file mixes both roles, `OPENINTENT.md` names the declarations or regions that control human choices.

An LLM may repair an implementation or its proof when a checker fails. It must not quietly weaken a mapped claim, add an assumption or unfinished placeholder, narrow the cases it covers, or break the link between a checked model and the software that claims to realize it. Such a change returns to intent shaping unless the mapped source already delegates that choice.

The project configures CI to run its checker and reject unfinished proofs or assumptions it has not accepted. The implementation and review handoffs name the exact checked claims, their assumptions, the software or protocol tied to them, and anything important the checker did not examine. A human still judges whether the formal claim says the right thing. Projects continue to use tests, benchmarks, devices, and direct human experience for qualities that formal proof does not cover. Formal proof remains optional.

## Carry active work

The implementation LLM carries the purpose, next steps, progress, discoveries, decisions, checks, and evidence in its chat and native plan while it works. The human steers the product, and the LLM keeps these working records current.

Before the branch reaches review, the LLM puts each result where future work will naturally find it:

- Lasting product choices go into the mapped intent source.
- Executable guarantees go into tests, models, benchmarks, machine-checked proofs, or other checks.
- Useful implementation or operations knowledge goes into the repository's normal engineering sources.
- Review evidence goes into the pull request or handoff.

When work must cross a chat boundary, the LLM leaves the smallest self-contained temporary handoff that lets a fresh LLM resume from the repository without the old chat. It preserves the purpose, current state, relevant discoveries and decisions, unresolved human choices, checks and evidence, recovery information, and next steps. The LLM keeps it current and removes or squashes it before merge unless the project deliberately wants to keep it.

## Add it to a repository

- Adapt [templates/OPENINTENT.md](templates/OPENINTENT.md) at the repository root. Map the sources the project already has instead of reorganizing them for OpenIntent.
- Fold [templates/AGENTS.md](templates/AGENTS.md) into the repository's agent instructions.
- Make the two skill directories available to the LLMs that implement and review changes. The agent instructions carry the essential rules when a tool cannot load skills.
- If the Git host supports them, adapt the pull-request and `CODEOWNERS` templates under [templates](templates/).

The implementation LLM prepares a branch, a second LLM reconstructs the intent from the repository and reviews that branch, CI checks facts it can determine, and a human controls the upstream merge.

## What lives here

- [OPENINTENT.md](OPENINTENT.md) makes this repository follow its own method.
- [MANIFESTO.md](MANIFESTO.md) states why OpenIntent exists.
- [openintent-implement](skills/openintent-implement/SKILL.md) guides the LLM that changes intent and code.
- [openintent-review](skills/openintent-review/SKILL.md) guides an independent, read-only review.
- [templates](templates/) show the small amount of wiring an intent-based repository needs.

OpenIntent keeps transient work lightweight, but it must not lose context. Before review, the implementation LLM moves lasting choices into the mapped specs, media, models, or other sources that future humans must understand.
