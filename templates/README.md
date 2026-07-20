# OpenIntent templates

Copy these files into an adopting repository and replace every angle-bracketed
placeholder. HTML comments explain what to write and may be removed.

## Minimum adoption set

```text
templates/AGENTS.md       -> AGENTS.md
templates/intent-index.md -> intent/index.md
templates/product.md      -> intent/product.md
templates/capability.md   -> intent/capabilities/CAP-<NAME>.md
templates/change.md       -> changes/CHG-<DATE>-<NAME>/change.md
```

Use the other templates when the product needs them:

- [repository-index.md](repository-index.md) when one repository contains
  several products; if the root index also serves one product, append that
  product's authority, artifact, target, change, and gap sections from
  [intent-index.md](intent-index.md);
- [capability-index.md](capability-index.md) and
  [capability-topic.md](capability-topic.md) when one capability needs a routed
  directory instead of one file;
- [quality.md](quality.md) for a measurable rule that spans capabilities;
- [profile.md](profile.md) for reusable workload, device, platform, topology,
  or failure conditions;
- [reference.md](reference.md) when exact checked-in visual, audible, protocol,
  schema, fixture, diagram, or other content forms part of the contract;
- [glossary.md](glossary.md) when several artifacts share an ambiguous product
  term;
- [decision.md](decision.md) for a durable product choice and its reason;
- [plan.md](plan.md) for broad, risky, or multi-session technical work;
- [discovery.md](discovery.md) when studying an existing implementation;
- [evidence.md](evidence.md), copied once per component or composition target
  and revision, before a reviewer calls that target conformant; and
- [review-checklist.md](review-checklist.md) during intent and conformance review.

Do not keep a blank template in `intent/` as if it were an accepted artifact.
Create an artifact when someone can name its real product job.

## Template rules

- Replace sample IDs with stable semantic IDs such as
  `CAP-PICKUP.retry-unknown-result`.
- Delete optional sections that do not apply.
- Do not delete a relevant section merely because the answer is unknown. Put the
  question in the active change and keep the intent draft.
- Write clear intent before implementation when practical. Update affected
  intent on the working branch when implementers find a product gap.
- Track intent and implementation checkpoints separately.
- Track each implementation target and revision separately.
- Register each product once and give every shared contract one owning product.
- Record every composition participant revision. Do not infer composition
  conformance from component results.
- Let profiles define reusable conditions, but keep duties and thresholds in
  product, capability, or quality rules.
- Give each normative supporting artifact one reference record, governing
  intent IDs, declared scope, allowed variation, and checked-in reviewable form.
- Split large capabilities by behavior topic, never by requirements versus
  scenarios versus evidence method.
- Keep product authority scopes and conflict resolvers in the intent index.
- Treat permission and transition tables as summaries that link to normative
  IDs, never as untagged requirements.
- Do not add implementation architecture to product or capability files.
- Use `UNSPECIFIED` only for actor-visible variation that product authority
  accepts. Omit unobservable internal mechanics.
- Express every forbidden outcome with a `MUST NOT` rule.
- Include each requirement ID in automated evidence names or adjacent comments.
- Use a normative scenario's more specific ID when a check targets that case.
- Keep actual test results in `evidence.md`, not in accepted intent.

The [specification](../SPECIFICATION.md) controls when a template and the
standard disagree.
