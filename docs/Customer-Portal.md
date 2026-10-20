# Customer Portal

<span class="ab-pill stub">STUB</span>

> **Stub — Phase 2 content.** No wiki-source-of-truth defined yet; canonical
> docs are the AquaButler-Server `auth/` and `portal/` directories.

## What it does

Per-customer identity, JWT, audit-log receipt, mobile + web surfaces.

- **Per-customer identity** — Supabase manages customer accounts; each
  customer is mapped to one or more AquaButler units (typically one).
- **JWT auth** — short-lived tokens scoped to the customer's UUID; refresh
  tokens are device-bound.
- **Audit log** — every customer-visible action (set temperature, run pump,
  service mode entry) is logged to Supabase for warranty + dispute
  resolution.
- **Mobile + web surfaces** — same backend, two clients (Flutter mobile +
  React web). Theming per
  [`AquaButler-Server/docs/wiki/canonical-messages.md`](https://github.com/ultron-aquabutler/AquaButler-Server/blob/main/docs/wiki/canonical-messages.md).

## See Also

- [`AquaButler-Server/auth/`](https://github.com/ultron-aquabutler/AquaButler-Server/tree/main/auth)
  — auth + JWT layer
- [`AquaButler-Server/portal/`](https://github.com/ultron-aquabutler/AquaButler-Server/tree/main/portal)
  — customer-facing web + mobile
- [`AquaButler-Server/docs/wiki/canonical-messages.md`](https://github.com/ultron-aquabutler/AquaButler-Server/blob/main/docs/wiki/canonical-messages.md)
  — brand rules + vocabulary lock

## Status

Content authoring tracked under kanban `t_b2740d21` (Phase 2 wiki content).