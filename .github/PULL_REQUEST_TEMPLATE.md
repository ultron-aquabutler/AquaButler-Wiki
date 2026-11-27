## Paired Obsidian vault write (REQUIRED — kanban t_67e61ff8)

Wiki PRs that land on AquaButler-Wiki MUST have a paired write to the canonical Obsidian vault path `Homelab/10-Services/AquaButler/...` before merge. Per-directory mirrors under `docs/wiki/` are retired.

The vault path above is **vault-relative** — it is resolved through `mcp__obsidian__write_doc` (or REST `http://obsidian.loc.wallacearizona.us:27123`), not as a host directory. Always use the vault-relative form beginning `Homelab/…`; a host-local path such as `~/Obsidian/Vault/...` points at a different, non-canonical tree on some hosts and will not find the page.

The vault is an NFS export of a plain directory tree — **it is not a git repository**, so there is no "vault commit SHA". Reference a paired write by its **vault path plus the on-disk sha256** of the written file.

- [ ] **Linked Obsidian vault write** on `Homelab/10-Services/AquaButler/...` — paste the vault-relative path, the on-disk sha256, and a short description of what was written.
- [ ] **Vault write path confirmed** — paste the `mcp__obsidian__write_doc` → `mcp__obsidian__read_doc` → `mcp__obsidian__search_vault` round-trip result (marker + on-disk sha256) proving the write path works at PR time.

**Both boxes must be checked** for merge. Phase-1-style legacy waivers must be approved by Bryan in a kanban comment on `t_c879dda4` or later.

---

## Summary

<!-- One-paragraph summary of what this PR changes. -->

## Pages touched

<!-- Bullet list of every `docs/*.md` page touched, with the canonical vault path it mirrors to. -->

## Vault mirror status

<!-- For each page touched, the canonical Obsidian vault path it now mirrors + on-disk sha256. -->

## Build verification

<!-- Paste the output of `mkdocs build --strict` from your worktree. -->

## Preview URL

<!-- Paste the GitHub Pages preview URL (fork Pages at `https://ultron-aquabutler.github.io/AquaButler-Wiki/`). -->

---

## Out of scope (do NOT include in this PR)

- [ ] Porting upstream wiki content verbatim (paraphrase only, with attribution)
- [ ] Custom fonts, logo swaps, or graphic design (graphic-designer handoff pending)
- [ ] Home Assistant YAML examples (deferred to v1.1 per kanban `t_3fd66d12`)
- [ ] Nixie DIY controller content (not in our scope)
