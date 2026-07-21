# OpenIntent

OpenIntent treats human-owned intent as source and LLM-written code as a replaceable result of that source.

Version 0.1 uses repository files, ordinary Git branches, two LLM skills, normal CI, and human approval.

## How a project uses it

1. Keep intent beside the code in the same repository. Intent may live in prose, images, recordings, prototypes, formal models, measurements, examples, or any other useful medium.
2. Add an `OPENINTENT.md` map. The map tells humans and LLMs which sources control each product choice and which evidence can test it.
3. Wire the workflow into `AGENTS.md` or the repository's equivalent instructions.
4. Let an implementation LLM work on a normal branch. It reads intent first, keeps the active plan and progress in the chat, revises intent when the work uncovers missing choices, and implements the current intent.
5. Let a separate LLM review the finished branch against the finished intent.
6. Let normal CI check deterministic facts and let a human approve the branch upstream.

Git keeps drafts, branches, commits, rebases, squashes, temporary handoffs, and failed experiments. Each project decides what deserves a lasting place.

## Carry active work

The implementation LLM carries the purpose, next steps, progress, discoveries, decisions, checks, and evidence in its chat and native plan while it works. The human steers the product, and the LLM keeps these working records current.

Before the branch reaches review, the LLM puts each result where future work will naturally find it:

- Lasting product choices go into the mapped intent source.
- Executable guarantees go into tests, models, benchmarks, or other checks.
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
