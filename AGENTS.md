# OpenIntent agent guide

This file is the canonical entry point for agents working in this repository.

## Read first

1. Read `SPECIFICATION.md` for normative rules.
2. Read the guide that covers the task in `docs/`.
3. Read only the templates, prompts, roles, and example files that the task
   touches.

`SPECIFICATION.md` wins when a guide, template, prompt, role card, or example
disagrees with it. Report the conflict instead of silently choosing a side.

## Repository purpose

OpenIntent defines a Markdown and Git method. It does not ship a coding agent,
CLI, parser, schema, hosted service, or vendor adapter.

Do not add tooling to solve a problem that clear repository rules can solve.
Record possible tools in `docs/evolution.md` until real project use shows that
the method needs them.

## Change rules

- Keep normative rules in `SPECIFICATION.md`; keep explanations in `docs/`.
- Keep `AGENTS.md` short and route agents to authoritative files.
- Keep templates consistent with every normative rule.
- Use the parcel locker example to test each workflow or artifact change.
- Use stable OpenIntent terms from `SPECIFICATION.md`.
- Use semantic requirement IDs; never use position numbers such as `R1`.
- Preserve the rule that intent should lead when practical and may evolve while
  people or agents implement and test.
- Keep intent and implementation checkpoints separate. Do not imply that
  accepted intent has already shipped.
- Treat code, tests, examples, and prior Git history as evidence, not product
  intent.
- Do not bind the method to an AI vendor, programming language, framework, or
  storage system.
- Do not add machine-readable metadata unless Markdown readers can still use the
  complete method without a tool.

## Review before finishing

- Follow `docs/maintainer-audits.md` for broad contract changes and record any
  problem that remains.
- Check every changed link and every referenced path.
- Check that a smart reader can identify the actor, action, conditions, and
  result in each normative sentence.
- Check that templates do not hide product requirements in implementation plans.
- Check that examples cover failure, permissions, concurrent actions, and
  recovery where relevant.
- Check that implementation discoveries can update proposed intent without
  granting code or an agent product authority.
- Search for vendor-specific assumptions and replace them with neutral terms.
