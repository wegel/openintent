# Repository intent index

| Field | Value |
| --- | --- |
| Repository | `<name>` |
| OpenIntent version | `0.1` |
| Accepted branch | `<branch>` |
| Last reviewed | `<YYYY-MM-DD>` |

This file routes readers across products. It does not define product behavior.

## Product authority registries

| Product or shared scope | Registry | Conflict resolver |
| --- | --- | --- |
| `PROD-<NAME>` | `<product index path or registry path>` | `<person>` |

## Products

| Product ID | Title | Product index | Intent root | Authority scope | Implementation targets | Depends on | Triggers |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `PROD-<NAME>` | `<product title>` | `<path>/index.md` | `<path>` | `<registry scope>` | `<IMPL IDs>` | `<product IDs or none>` | `<search terms>` |

## Shared and cross-product contracts

<!-- Give each contract one owner. Consumers link to the owner's intent IDs and
must not copy the rules. -->

| Contract | Owning product | Governing intent IDs | Consuming products | Compatibility or failure consequence |
| --- | --- | --- | --- | --- |
| `<boundary name>` | `PROD-<OWNER>` | `<intent IDs>` | `<product IDs>` | `<observable consequence>` |

## Cross-product active changes

| Change | Coordinator | Affected products | Intent checkpoint | Proposed revision | Path |
| --- | --- | --- | --- | --- | --- |
| `CHG-<DATE>-<NAME>` | `<person>` | `<product IDs>` | Draft | `<commit or pending>` | `<change path>` |

## Repository-wide implementation compositions

<!-- Keep product-local targets in their product indices. List a composition
here when it crosses product boundaries. -->

| Target ID | Scope | Owner | Components and external participants | Revision | Checkpoint | Latest evidence |
| --- | --- | --- | --- | --- | --- | --- |
| `IMPL-<COMPOSITION>` | `<supported assembly>` | `<person or team>` | `<target and external-system IDs with exact revisions>` | `<composition manifest revision>` | Unknown | `<path or none>` |
