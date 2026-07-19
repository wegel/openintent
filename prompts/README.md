# Vendor-neutral prompts

These prompts describe bounded tasks with ordinary Markdown. They do not depend
on slash commands, a model vendor, a coding-agent product, or hidden session
state.

Choose one prompt and replace every angle-bracketed placeholder. Include the
change ID, implementation target when the task touches one, and context paths
instead of asking an agent to read the whole repository.

| Task | Prompt |
| --- | --- |
| Draft or revise a product change | [draft-change.md](draft-change.md) |
| Challenge proposed intent | [review-intent.md](review-intent.md) |
| Implement and refine one change | [implement-change.md](implement-change.md) |
| Check conformance and write evidence | [verify-conformance.md](verify-conformance.md) |
| Study an existing implementation | [discover-existing-system.md](discover-existing-system.md) |
| Audit and curate the intent tree | [curate-intent.md](curate-intent.md) |

A prompt never grants more product authority than `AGENTS.md` grants. When chat
and repository intent disagree, the agent reports the conflict.
