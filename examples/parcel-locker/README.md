# Parcel locker product repository example

This fictional project shows how one OpenIntent repository can govern a parcel
pickup product and route a separately owned Courier Console draft. The example
includes:

- bearer-token permissions without exposing recipient identity;
- two valid pickup attempts racing for one parcel;
- retries after a locker controller loses replies;
- a product invariant that blocks reassignment while an open result is unknown;
- an implementation discovery that sends intent back through product review;
- operator recovery with an audit trail;
- a technical plan that stays outside product intent;
- a completed fictional evidence record with stated limits;
- two service component targets whose different conformance results remain
  separate;
- an independently governed second product with a modular capability;
- one operating profile that defines reproducible conditions without hiding a
  performance threshold;
- one JSON artifact that governs a controller request shape;
- one draft SVG that governs visual relationships across phone and desktop
  stop cards; and
- a pickup-site composition that remains `Unknown` despite conformant service
  component evidence.

No app or service implementation ships in this example. The evidence runs and
build IDs are illustrative records from a fictional harness. They demonstrate
the shape and honesty expected from evidence; they do not certify code in this
repository.

## Read order

1. [AGENTS.md](AGENTS.md)
2. [intent/index.md](intent/index.md)
3. [intent/product.md](intent/product.md)
4. [intent/capabilities/CAP-PICKUP.md](intent/capabilities/CAP-PICKUP.md)
5. [intent/qualities/QLT-AUDIT.md](intent/qualities/QLT-AUDIT.md)
6. [PROF-PEAK-SITE](intent/profiles/PROF-PEAK-SITE.md) and
   [REF-CONTROLLER-OPEN-V7](intent/references/REF-CONTROLLER-OPEN-V7.md)
7. [the Courier Console product index](products/courier-console/intent/index.md)
   and its modular
   [capability index](products/courier-console/intent/capabilities/CAP-COURIER-EXCEPTIONS/index.md),
   then its draft
   [visual reference](products/courier-console/intent/references/REF-COURIER-STOP-CARD.md)
8. [changes/CHG-20260701-CONTROLLER-UNCERTAINTY/change.md](changes/CHG-20260701-CONTROLLER-UNCERTAINTY/change.md)
9. The change [plan](changes/CHG-20260701-CONTROLLER-UNCERTAINTY/plan.md) and
   [evidence](changes/CHG-20260701-CONTROLLER-UNCERTAINTY/evidence.md)

Read [discovery/controller-timeouts.md](discovery/controller-timeouts.md) to see
how a brownfield team kept code observations, confirmed intent, unknown behavior,
and conflicting sources separate before accepting the change.

## What the example tests in OpenIntent

The product contract says what another implementation must preserve. It does not
say which database, queue, process topology, or programming language to use.

The plan chooses one store update and a durable work queue. A replacement
implementer may discard both choices if it preserves every named invariant and
meets every requirement.

The implementation plan also records a late controller result discovered during
testing. The author revised the reconciliation intent, product authority
accepted the material edit, and implementation continued. The example treats
intent-first work as a strong default and later intent edits as normal work.

The intent index records the current 5.x service and the legacy 4.8 service as
different implementation targets. Evidence supports conformance only for the
5.x target. The [legacy evidence](changes/CHG-20260701-CONTROLLER-UNCERTAINTY/evidence-legacy.md)
keeps the 4.8 target's failed and untested rules visible instead of borrowing
the 5.x result.

The index also registers `IMPL-PICKUP-SITE-R7` as a composition of the service,
a physical controller, and the regional audit interface. Its checkpoint stays
`Unknown` because the fictional evidence checks a service component against
simulators, not the assembled site.

The draft Courier Console owns its product choices and consumes only the pickup
rules named by the Parcel Pickup Coordinator. The example leaves its missing
interface and platform choices open instead of turning guesses into accepted
intent. Its capability uses an index and behavior-topic file so one product can
grow without forcing every reader to load every rule.

The Courier Console also carries `REF-COURIER-STOP-CARD` and its SVG source as a
Draft proposal. Text defines fields, permissions, states, and accessibility
meaning. The drawing defines only the proposed visual grouping and reading
order, with explicit phone, desktop, localization, and large-text variation.

`PROF-PEAK-SITE` gives reviewers the exact load and topology to reproduce.
`QLT-AUDIT.event-availability` still owns the passing threshold.
`REF-CONTROLLER-OPEN-V7` and its JSON source govern a request shape that prose
alone would make harder to compare. The parent pickup rules still own timing,
identity, and secret handling.

The change record summarizes a policy edit but does not copy its normative text.
In a real Git repository, the branch diff would show the exact edit to
`CAP-PICKUP`. This static example shows the accepted end state.

A completing commit would preserve the trace with trailers such as:

```text
Change: CHG-20260701-CONTROLLER-UNCERTAINTY
Implements: CAP-PICKUP.retry-unknown-result,
 CAP-PICKUP.reconcile-unknown-result
```

## Fictional scope

An upstream fulfillment system has already placed the parcel in a compartment
and registered a pickup assignment. This product coordinates pickup only. It
does not route couriers, choose a locker, deliver the token, or control locker
firmware.
