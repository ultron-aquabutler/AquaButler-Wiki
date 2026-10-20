# Rotary Display

<span class="ab-pill stub">STUB</span>

> **Stub — Phase 2 content.** Canonical vocabulary per
> [`AquaButler-Server/docs/wiki/canonical-messages.md`](https://github.com/ultron-aquabutler/AquaButler-Server/blob/main/docs/wiki/canonical-messages.md)
> (locked 2026-10-19, kanban `t_3790f4b4`).

## What it is

240×240 SPI panel, rotary encoder + center press button.

## Modes

- **Status** (default, LIVE page + SYSTEM page)
- **Service** (PIN-gated)
- **Manual** (SELECT / EDIT / CONFIRM sub-states)

## Color coding

| Color | Condition |
|--------|-----------|
| GREEN | Live data |
| YELLOW | Stale data (60s < Δt < 120s) |
| RED | Error / offline / stale ≥120s |
| ORANGE | Service-mode active banner |

## See Also

- [`AquaButler-Server/docs/wiki/canonical-messages.md`](https://github.com/ultron-aquabutler/AquaButler-Server/blob/main/docs/wiki/canonical-messages.md)
  — locked strings (44-string inventory as of 2026-10-19)
- `src/rotary_display/rotary_display/modes/*.py` — rotary display firmware

## Status

Content authoring tracked under kanban `t_b2740d21` (Phase 2 wiki content).