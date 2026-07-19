# Contributing to OpenIntent

OpenIntent should grow from concrete project use. Proposals based only on a new
tool's capabilities should wait until users show that the method itself needs a
change.

## Before proposing a change

1. Read `SPECIFICATION.md` and the related guide.
2. Test the idea against the parcel locker example.
3. Describe a real failure that the current text causes.
4. State whether the proposal changes a normative rule, explanation, template,
   prompt, role card, or example.
5. Check that a project can still use the result with Markdown, Git, and
   `AGENTS.md` alone.
6. Run the relevant checks in `docs/maintainer-audits.md`.

## Proposal content

A normative proposal should include:

- the reader or project that faces the problem;
- a minimal example that exposes the problem;
- the exact rule changes;
- compatibility effects for existing adopters;
- alternatives and their costs;
- template and example updates; and
- evidence from use when available.

Open questions should stay visible. An author should not hide a product or
governance choice inside polished wording.

## Review standard

Reviewers check clarity, vendor neutrality, human readability, context cost,
traceability, and whether the rule keeps intent separate from implementation.
Before the first public release, normative changes need maintainer acceptance
recorded in the repository review. When the project has a maintainer other than
the author, that maintainer reviews the normative edit. Editorial fixes need one
maintainer review.

The first public release remains version 0.1. A maintainer must record a passing
result for every check in `docs/maintainer-audits.md` before publication. The
publication change sets the project status to `Public draft` without increasing
the version.

After publication, normative changes need public review and maintainer
acceptance. The project will define stricter version and standards rules only
after real contributors show which rules they need.

Until then, Git issues and pull requests provide the review record.

## Commit practices

Keep each commit focused. Do not add generated vendor adapters to this
repository. Do not add contributor trailers unless the contributor asks for
them.
