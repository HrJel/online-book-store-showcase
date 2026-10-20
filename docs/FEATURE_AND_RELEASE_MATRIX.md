# Online Book Store — Feature inventory, acceptance criteria and release gates

> Updated 2026-10-20. **Do not confuse a Cloudflare Pages deployment marked successful with a successful application feature test.** Current Pages websites are earlier documentation builds; verified production deployment of the new application is **not** recorded.

## Evidence legend

- Public status = what exists in this GitHub repo
- Source-documented = described in a separate reviewed implementation, not copied
- Staged foundation = authored outside repository and not deployed
- Planned / NOT IMPLEMENTED = must not be marketed as shipped

**Public repository audit:** Repository contains public documentation, disclaimers and metadata only. App assets in a separate prepared package have not been published to this repository.

## Project-specific feature matrix

| Feature / module | Honest implementation status | Completion/production acceptance criteria |
| --- | --- | --- |
| Book catalog and metadata | Independent sample data in staged UI; public docs only | ISBN/author/title validation, inventory schema, admin content approvals. |
| Search and discovery | Prototype scope; not live as app | Fast, escaped search, pagination, filters, accessibility. |
| Wishlist and basket | Simulated only | Signed/account-scoped basket with concurrency and stock changes. |
| Guest/customer login | Cloudflare auth foundation prepared, not deployed | Customer login/registration, recovery/MFA and role separation. |
| Prices and taxes | Planned | Currency rounding, country tax and pricing consistency. |
| Checkout and payment | NOT IMPLEMENTED | Hosted provider checkout, webhook signature verification, idempotent paid/failed/refund states. |
| Inventory reservation | NOT IMPLEMENTED | Transactional reservation/release after payment/timeout. |
| Orders, shipping and returns | Example orders only; not real transactions | Customer receipts, fulfillment tracking, refund and privacy operations. |

## Platform and integration truth table

| Deliverable | Status |
| --- | --- |
| Public GitHub docs | Published |
| New independently authored frontend files | Not yet in this GitHub repo |
| Authenticated Pages Worker runtime | Prepared separately, not deployed |
| Pages project / documentation site | Exists; documentation deployment successful |
| Turnstile widget per hostname | Configured at Cloudflare account level; challenge not live-verified in app |
| D1 AUTH_DB shared binding | Provisioned; isolated domain/business schema absent |
| Administrator secret and session login end-to-end | Not verified; no claim user can currently sign in |
| Fully featured product backend | Not built/verified in this public repo |
| Native iOS/Android/macOS signed releases | Not published or verified by this public repo |

## Definition of done for any module

- Domain entity/model, migration, API schema, error states and data ownership are documented.
- Server performs authentication, authorization, validation and idempotency where required.
- Unit, integration and browser end-to-end tests demonstrate success and failure behaviors.
- Observability records meaningful non-sensitive telemetry, with alerts, rollback and retention defined.
- Owner approves any client IP and third-party assets before public release.
- Claims in this matrix are updated based on reproducible test artifacts, not screenshots or roadmap promises.

## Prioritized milestones for Online Book Store

1. Publish only approved independent application source and verify actual git contents.
2. Configure per-project `ADMIN_USERNAME` and strong `ADMIN_PASSWORD` secrets, then deploy the prepared Worker to **staging**. Verify Siteverify response, session and D1 isolation.
3. Build the first two missing business modules behind an audited, least-privilege API, with synthetic fixture data.
4. Complete every critical feature above, API integration and negative/security test.
5. Perform deployment rehearsal and publish real release metadata; only then change a feature status to **production-ready**.

For architecture and language inventory see [Technical reference](TECHNICAL_REFERENCE.md). For security and on-call readiness see [Security and operations](SECURITY_AND_OPERATIONS.md).

**Jelvan® credit:** [Developed and Designed by Jelvan®](https://portfolio.jelvan.pro) — independent public portfolio work, not a claim of ownership of private client code.
