# MQTT Bindings

<span class="ab-pill stub">STUB</span>

> **Stub — Phase 2 content.** Canonical schema doc is
> `~/AquaButler-Server/VISION.md` and the new
> `docs/wiki/mqtt-topic-schema.md` (to be authored under kanban card
> `t_5cd77dad` / gap report Gap 8).

## Topic shape (preview)

```
pool/<customer_id>/<stream>/<...>
```

Per-customer isolation: every topic is namespaced under the customer's UUID.

## Streams (preview)

| Stream | Direction | Purpose |
|--------|-----------|---------|
| `state` | pub | Current state of every circuit, pump, heater, chem sensor |
| `command` | sub | Customer-issued commands (turn on pump 1, set heater to 80°F) |
| `config` | both | Per-customer config (timezone, units, alert prefs) |
| `health` | pub | Device health, OpenBalena heartbeat, last-seen timestamps |
| `audit` | pub | Service mode entries, manual-mode changes, admin actions |

## See Also

- [`AquaButler-Server/VISION.md`](https://github.com/ultron-aquabutler/AquaButler-Server/blob/main/VISION.md)
  — full architecture spec
- Upstream wiki: [Bindings-Integrations](https://github.com/tagyoureit/nodejs-poolController/wiki/Bindings-Integrations)
  — protocol-level reference

## Status

Full content authoring tracked under kanban `t_5cd77dad` (Gap 8 follow-up).