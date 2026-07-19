Project: OpenIntent

Your task is to design and implement a new open-source project from scratch.

Do not build a coding agent or a CLI.

Instead, design an open standard for AI-native software development.

The project should define a specification format, repository structure, workflow, documentation, templates, and agent conventions that any coding agent can follow.

Think of this project as defining the equivalent of Git’s workflow or the IETF’s RFC process, rather than another software tool.

⸻

Vision

Traditional software development treats source code as the authoritative artifact.

OpenIntent should instead treat product intent as the authoritative artifact.

Humans primarily edit specifications.

Coding agents primarily edit implementations.

Implementations are evaluated against specifications and should ideally be replaceable or regenerable.

The goal is to make source code an implementation artifact rather than the primary representation of a software system.

⸻

Important principle

The project must not be tied to any specific AI vendor.

It should work equally well with:

* Codex
* Claude Code
* Cursor
* Gemini CLI
* GitHub Copilot
* future coding agents

The standard should remain useful even if entirely different coding agents appear in the future.

⸻

Scope

The project defines a methodology.

It does not initially define tooling.

Avoid creating a CLI unless absolutely necessary.

Avoid introducing machine-readable schemas unless they clearly improve the methodology itself.

The first version should work using nothing more than:

* Markdown
* Git
* AGENTS.md
* repository conventions

Tooling can always be added later if real-world usage demonstrates the need.

⸻

Core philosophy

The specification should define:

* system purpose
* product behavior
* observable behavior
* domain concepts
* invariants
* workflows
* state transitions
* permissions
* assumptions
* failure behavior
* quality constraints
* acceptance criteria

The specification should normally not define:

* programming language
* framework
* persistence technology
* internal architecture
* module decomposition
* class hierarchy
* algorithms
* implementation mechanics

Implementation decisions should be delegated to coding agents whenever possible.

⸻

Primary objective

The resulting repository should become an open standard that projects can adopt.

A developer starting either a new project or an existing one should be able to adopt OpenIntent simply by copying the repository structure and following the methodology.

⸻

Repository

Design the repository itself.

It should primarily contain:

* documentation
* methodology
* templates
* examples
* agent conventions
* reusable prompts

Avoid building unnecessary software.

⸻

Repository structure

Design the repository structure.

Current idea:

OpenIntent/

README.md
AGENTS.md
SPECIFICATION.md
docs/
templates/
examples/
prompts/
roles/

Redesign this freely if a better structure exists.

⸻

AGENTS.md

AGENTS.md should be the canonical entry point for coding agents.

It should:

* explain the methodology
* define the workflow
* point agents toward authoritative artifacts
* remain intentionally concise

It should not duplicate the entire methodology.

⸻

Specification format

Design the specification format.

Think deeply about the artifact types.

Possible artifacts include:

* product
* glossary
* capabilities
* quality requirements
* decisions
* scenarios
* examples
* changes
* questions
* evidence

Determine:

* which artifacts should exist
* what belongs in each
* how they relate

Question everything.

⸻

Capability specification

Design the ideal capability template.

Current thoughts:

Purpose

Scope

Actors

Requirements

Invariants

Flows

Failure handling

Concurrency

Security

Examples

Forbidden scenarios

Delegated implementation decisions

Acceptance evidence

Improve this.

Remove sections.

Merge sections.

Add missing concepts.

⸻

Semantic vocabulary

Design the normative language.

Current ideas:

MUST

MUST NOT

SHOULD

MAY

ASSUME

PREFER

UNSPECIFIED

UNRESOLVED

NON-GOAL

RATIONALE

Determine whether this vocabulary is sufficient.

⸻

Workflow

Design the complete development workflow.

Think through:

new feature

behavioral change

review

implementation

verification

acceptance

traceability

migration

The workflow should be natural for both humans and coding agents.

⸻

Agent roles

Design the role model.

Current thoughts:

Specifier

Specification reviewer

Implementer

Conformance reviewer

Legacy discovery agent

Determine whether this is the correct decomposition.

⸻

Existing project migration

Design how an existing codebase should migrate.

Important principle:

Current implementation is not automatically the intended behavior.

The methodology should distinguish:

descriptive behavior

intended behavior

unknown behavior

conflicting behavior

Migration should preserve this distinction.

⸻

Validation

Design the validation philosophy.

Without requiring formal verification.

Think about:

structural review

semantic review

implementation review

traceability

acceptance evidence

future formalization

The methodology should be useful today without requiring specialized tooling.

⸻

Adapters

The methodology should be centered around AGENTS.md.

Determine whether additional agent-specific files are actually necessary.

If they are, they should be considered optional compatibility layers rather than canonical artifacts.

⸻

Traceability

Design an elegant traceability model connecting:

requirements

changes

implementation

tests

verification evidence

Avoid heavyweight enterprise requirements management systems.

Keep the methodology lightweight and understandable.

⸻

Context

One important objective is minimizing context size for coding agents.

Design how projects should organize specifications so an implementation agent only needs to read the relevant subset.

Do this through repository organization rather than tooling.

⸻

Examples

Include at least one realistic example project demonstrating the methodology.

Avoid Todo applications.

Choose something involving:

* concurrency
* retries
* permissions
* failure recovery
* meaningful invariants

⸻

Documentation

The repository should feel like an RFC.

It should define the methodology itself.

Possible top-level documents:

Introduction

Terminology

Design philosophy

Repository layout

Artifact definitions

Workflow

Migration guide

Examples

Future directions

Determine the best structure.

⸻

Future evolution

Assume no tooling initially.

However, design the methodology so that future tooling could naturally emerge, for example:

* validation
* context generation
* traceability
* specification review
* conformance checking

without changing the methodology itself.

The methodology should come first.

Tooling should merely automate parts of it later.

⸻

Research expectations

Before designing anything:

1. Research existing approaches such as OpenSpec, GitHub Spec Kit, Kiro, codemix, BMAD, and related specification-driven development systems.
2. Identify their strengths and weaknesses.
3. Critically analyze every idea in this prompt.
4. Replace any part of this proposal if a better design exists.

Do not optimize for agreement with this prompt.

Optimize for creating the best possible open standard.

Challenge assumptions.

Prefer long-term elegance over familiarity.

The resulting repository should feel like the first serious attempt at defining an open, vendor-neutral standard for specification-as-source software development in the age of coding agents.
