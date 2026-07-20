# <Capability title>

| Field | Value |
| --- | --- |
| ID | `CAP-<NAME>` |
| Status | Draft |
| Product authority scope | `<registry scope>` |
| Accepted change | `<change ID or pending>` |
| Last reviewed | `<YYYY-MM-DD>` |
| Read with | `<linked glossary, qualities, profiles, references, decisions, or adjacent capabilities>` |

## Outcome and boundary

`<Actor>` can `<outcome>`. This capability begins when `<boundary event>` and
ends when `<terminal result>`. `<Adjacent capability or external system>` owns
`<excluded responsibility>`.

## Content map

<!-- List every normative topic file. Keep behavior that readers commonly need
together. Do not split requirements from their scenarios or acceptance maps.
When a topic uses a normative reference, its governing requirement still states
the semantic duty and why the exact property forms part of the boundary. -->

| Topic | Path | Owned intent IDs | Read with | Triggers |
| --- | --- | --- | --- | --- |
| `<behavior topic>` | `<topic>.md` | `<ID prefixes or exact IDs>` | `<context paths>` | `<search terms>` |

## Capability-wide actors and invariants

<!-- Keep only actors and invariants that several topics need. Topic-local
actors and rules stay in the owning topic file. Every normative invariant uses
a semantic ID and appears in an acceptance map. -->

### CAP-<NAME>.<invariant-slug> <Invariant title>

The `<concrete product actor>` MUST `<condition that survives every legal path>`.

## Capability-wide acceptance map

| Intent ID | Evidence needed |
| --- | --- |
| `CAP-<NAME>.<invariant-slug>` | `<cross-topic check>` |

## Open questions

- **OPEN QUESTION:** `<question>` Owner: `<person>`. Blocks: `<IDs or gate>`.
