# Audit and curate an OpenIntent tree

Act as the curator for `<product or repository scope>`.

## Read

1. `<nearest AGENTS.md>`
2. `<root index and affected product indices>`
3. `<artifact paths or tree-wide scope>`
4. `<active change records>`

## Goal

Keep the product contract small, linked, findable, and internally consistent
without changing product meaning.

## Allowed writes

- meaning-preserving repairs to links, paths, ID references, duplicated text,
  and formatting;
- `intent/index.md` context routes; and
- review findings in `<project review location>`.

Do not change a product duty without creating or updating a change record and
asking product authority.

## Checks

1. Check required metadata, allowed states, semantic ID uniqueness, links,
   scenario parents, product ownership and dependencies, authority registries,
   and component and composition targets.
2. Find permission, state, transition, and flow rows that state product duties
   without governing normative IDs. Find normative scenarios missing from
   acceptance maps.
3. Check glossary terms for missing definitions or competing names.
4. Measure large capability files and common context paths. Propose behavior-topic
   splits that preserve IDs and keep requirements with scenarios and acceptance.
5. Check operating profiles for hidden duties or results and check normative
   supporting artifacts for missing governing IDs, scope, variation, or
   checked-in reviewable forms.
6. Find active changes with missing owners, stale checkpoints, unresolved
   questions, or overlapping IDs that lack a recorded order or resolver.
7. For each target that claims conformance, find every applicable product
   invariant, requirement, or normative scenario without current evidence.
   Find evidence that names an old target or accepted intent revision.
8. For each composition target, verify every participant revision and reject
   borrowed component conclusions.
9. Enumerate actor-visible interfaces, events, errors, and states in scope.
   Record behavior that accepted intent does not cover.
10. Separate safe direct repairs from edits that can change product meaning.

## Return

- direct repairs made;
- product edits proposed but not made;
- broken or stale routes;
- missing authority scopes, target records, and unresolved overlaps;
- largest files and context paths;
- uncovered actor-visible behavior;
- target-specific missing or stale evidence; and
- next bounded action with an owner.
