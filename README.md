# OpenIntent

OpenIntent is a vendor-neutral standard for building software from product intent.
Humans maintain the product contract in Markdown. Coding agents build and review
implementations against that contract. Git records each proposed change and its
review history.

OpenIntent defines a method, not a coding agent, command-line program, or hosted
service. A project can adopt it with Markdown, Git, and a root `AGENTS.md` file.

> Project status: OpenIntent 0.1 is a pre-publication draft. It will remain 0.1
> through its first public release. Try it, report where it fails, and expect the
> standard to change before 1.0.

## The core idea

Source code can show what one implementation does. It cannot reliably show what
the product should do, which behavior is accidental, or which choices another
implementation may change. OpenIntent keeps those answers in a small set of
reviewed intent files.

Teams should write clear intent before implementation when they can. Working
software and tests will still reveal missing needs, constraints, and product
choices. OpenIntent lets intent and implementation evolve together while named
people retain authority over material product decisions.

A team may revise and review intent several times before anyone starts an
implementation. After work starts, implementers and reviewers may keep refining
intent as code and tests expose new facts.

An adopting project runs this loop:

```text
need or discovery
  -> proposed product intent
  -> product review
  -> implementation and tests
  -> intent revision when work exposes a gap
  -> conformance evidence
  -> record the target result, continue, or leave implementation pending
```

The loop may return to intent review many times. The same person or agent may
edit intent, code, tests, and evidence. Product authority still accepts material
product choices.

Each artifact uses semantic IDs and ordinary Markdown links. A reviewer can
follow one requirement through changes, test tags, Git trailers, and evidence
without a database or special parser.

Projects register who may accept each product scope. They also track each
implementation target separately, so a web service, device build, and supported
release line never share one misleading conformance state.

## Start here

- Read [SPECIFICATION.md](SPECIFICATION.md) for the normative standard.
- Read [docs/adoption.md](docs/adoption.md) to add OpenIntent to a new or
  existing project.
- Copy and adapt the files in [templates](templates/README.md).
- Study the [parcel locker example](examples/parcel-locker/README.md), which
  covers permissions, concurrent pickup attempts, retries, and recovery.
- Give every coding agent the project's root `AGENTS.md` as its first entry
  point.

The supporting guides explain the method in more depth:

- [Design principles](docs/design-principles.md)
- [Artifact model](docs/artifact-model.md)
- [How to write intent](docs/writing-intent.md)
- [Change workflow](docs/workflow.md)
- [Review and evidence](docs/review-and-evidence.md)
- [Maintainer audits for this standard](docs/maintainer-audits.md)
- [Existing project migration](docs/migration.md)
- [Agent portability](docs/agent-portability.md)
- [Prior work and design choices](docs/research.md)
- [How the standard can evolve](docs/evolution.md)

## What OpenIntent does differently

OpenIntent keeps the current product contract separate from both code and old
change records. Writers edit the contract directly on a Git branch, so Git
already supplies the proposed delta. They do not maintain a second copy that a
tool must merge later.

Accepted intent may precede implementation. The intent index tracks intent and
each implementation target separately, so `Accepted` means “the product requires
this” and does not pretend that every current build already conforms.

OpenIntent also separates four claims that teams often blur together:

- **Intended:** an accepted intent file says what the product should do.
- **Observed:** discovery notes show what someone measured in an implementation.
- **Unknown:** discovery notes say that available evidence cannot answer.
- **Conflicting:** discovery notes show that sources disagree and name each
  source.

No agent may turn observed behavior into intended behavior without a person who
owns that product choice accepting it.

## Repository map

```text
AGENTS.md          entry point for agents working on this standard
SPECIFICATION.md   normative OpenIntent 0.1 rules
docs/              explanations, adoption guidance, and research
templates/         copyable project artifacts
examples/          worked examples
prompts/           vendor-neutral task prompts
roles/             small responsibility cards, not agent personas
```

An adopting product uses the layout described in
[SPECIFICATION.md](SPECIFICATION.md#5-default-project-layout).

## Contributing

OpenIntent should improve through public use and concrete evidence. See
[CONTRIBUTING.md](CONTRIBUTING.md) before proposing a change to the standard.

## License

OpenIntent is available under the [MIT License](LICENSE).
