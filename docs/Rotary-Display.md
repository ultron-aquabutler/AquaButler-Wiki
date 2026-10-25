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
- **Cloud alert** (a detail screen, reached by holding the knob while a
  cloud-loss notice is showing — see
  [Losing Internet Connection](Losing-Internet-Connection.md))

## Cloud-loss notice

When the unit cannot reach the internet, a persistent banner appears along
the bottom of the status screen:

| Banner | Color | Meaning |
|--------|-------|---------|
| `CLOUD UNREACHABLE` | RED | The cloud link is down. Schedules keep running and the panel still works. |
| `SERVICE MODE` | ORANGE | A technician has put the unit into service mode. Not a fault. |
| `COMMISSIONING` | YELLOW | The unit is being installed. Not a fault. |

The banner never blocks the manual override menu — local control stays
fully available. See
[Losing Internet Connection](Losing-Internet-Connection.md) for what
customers see and what to do.

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