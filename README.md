# AquaButler Wiki

Customer-facing AquaButler documentation, built with [MkDocs Material](https://squidfunk.github.io/mkdocs-material/)
and deployed to GitHub Pages at **aquabutlers.com/wiki**.

This is the public AquaButler wiki — customers, installers, and partners land here.
Engineering source-of-truth docs live in the implementation repos:

- [`AquaButler-Hardware`](https://github.com/ultron-aquabutler/AquaButler-Hardware)
  — carrier board, schematics, BOM, enclosure, engineering architecture
- [`AquaButler-Server`](https://github.com/ultron-aquabutler/AquaButler-Server)
  — cloud side: Supabase, MQTT broker, customer portal, rotary-display firmware

## Repo workflow

This repo follows the AquaButler fork+PR pattern:

- Working fork: `ultron-aquabutler/AquaButler-Wiki`
- Canonical target: `brydenver2/AquaButler-Wiki`
- Per AquaButler-Server `AGENTS.md` "GitHub Workflow": code ships to fork first,
  PR to canonical, **only Bryan clicks Merge on the canonical repo**.

## Build locally

```bash
pip install mkdocs mkdocs-material
mkdocs serve     # http://localhost:8000
```

## Brand

Palette and locked vocabulary per
[`AquaButler-Server/docs/wiki/canonical-messages.md`](https://github.com/ultron-aquabutler/AquaButler-Server/blob/main/docs/wiki/canonical-messages.md)
(locked 2026-10-19). Logo asset is the interim submark
(`brand/aquabutler-submark-placeholder-2026-10-18.jpg`) until graphic-designer
handoff lands.

## Phase status

This is Phase 1: scaffold + 1 fully-written pilot page (Hardware Overview) +
9 page-stubs + GitHub Pages deploy. Phase 2 content authoring is tracked
under kanban `t_b2740d21` per
[`AquaButler-Hardware/docs/wiki-gap-2026-10-19.md`](https://github.com/ultron-aquabutler/AquaButler-Hardware/blob/main/docs/wiki-gap-2026-10-19.md).

---

*AquaButler™ — Backyard Butlers LLC.*