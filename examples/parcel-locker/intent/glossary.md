# Product glossary

| Field | Value |
| --- | --- |
| ID | `GLO-PARCEL-PICKUP` |
| Status | Accepted |
| Product authority scope | Parcel pickup behavior |
| Accepted change | `CHG-20260701-CONTROLLER-UNCERTAINTY` |
| Last reviewed | 2026-07-19 |

| Term | Meaning in this product | Allowed aliases | Avoid | Owned by |
| --- | --- | --- | --- | --- |
| **Assignment** | One parcel placed in one compartment for one pickup window | Pickup assignment | Order, delivery | `CAP-PICKUP` |
| **Pickup token** | A secret bearer value that authorizes a claim for exactly one assignment during its pickup window | Token | PIN, recipient identity | `CAP-PICKUP` |
| **Claim** | The product's exclusive grant that lets one valid pickup attempt request the assigned door to open | Pickup claim | Login, reservation | `CAP-PICKUP` |
| **Logical open request** | One intended door-open action for one claim, identified across all attempts by one request ID | Open request | Retry attempt | `CAP-PICKUP` |
| **Attempt** | One transmission of a logical open request to the locker controller | Controller attempt | Request | `CAP-PICKUP` |
| **Unknown open result** | The product cannot prove whether the controller executed a logical open request | Unknown result | Failure | `CAP-PICKUP` |
| **Collected** | The controller reported the assigned door open and later closed for the pickup session | Pickup complete | Parcel removed | `CAP-PICKUP` |
| **Site Recovery role** | Permission to inspect and resolve pickup state for named locker sites without reading raw pickup tokens | Site operator | Admin | `CAP-PICKUP` |
