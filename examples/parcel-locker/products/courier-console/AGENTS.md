# Courier Console agent guide

This file routes work for the draft Courier Console product.

## Authority

- Accepted branch: `main`
- Repository index: `../../intent/index.md`
- Product index and authority registry: `intent/index.md`
- Product intent root: `intent/`
- Implementation targets: `IMPL-COURIER-PHONE` and
  `IMPL-COURIER-DESKTOP`

The product remains Draft. Its files describe proposed intent, not accepted
product behavior or a shipped app.

## Read order

1. Read `../../intent/index.md` for repository products and owned contracts.
2. Read `intent/index.md` for this product's authority and routes.
3. Read the affected product and capability topic files.
4. Follow every consumed pickup rule to the Parcel Pickup Coordinator's owning
   file. Do not copy or reinterpret it here.

## Work rules

- Keep Courier Console choices under this product's named authority.
- Ask the Parcel Pickup Coordinator authority to accept any proposed change to
  an owned pickup rule.
- Keep an observed app behavior in discovery until product authority accepts
  it as intent.
- Keep each Courier Console target at `Unknown` until evidence names that app's
  revision and the proposed intent has become Accepted.
