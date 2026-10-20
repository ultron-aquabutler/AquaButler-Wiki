# API Reference

<span class="ab-pill stub">STUB</span>

> **Stub — Phase 2 content.** Canonical API surface is the AquaButler-Server
> customer portal API + the per-customer MQTT topology (see
> [MQTT Bindings](MQTT-Bindings.md)).

## HTTP API (preview)

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/v1/units` | GET | List units owned by the authenticated customer |
| `/v1/units/{uuid}` | GET | Unit detail (state, config, last-seen) |
| `/v1/units/{uuid}/command` | POST | Issue a command (turn on pump 1, set heater to 80°F) |
| `/v1/units/{uuid}/audit` | GET | Audit log for the unit |

All endpoints require a customer-scoped JWT (see
[Customer Portal](Customer-Portal.md)).

## MQTT API

See [MQTT Bindings](MQTT-Bindings.md) for the full topic schema. Summary:

```
pool/<customer_id>/state/...       (sub — current state)
pool/<customer_id>/command/...     (pub — customer commands)
pool/<customer_id>/health/...      (sub — device health)
```

## See Also

- Upstream
  [nodejs-poolcontroller-api Swagger](https://tagyoureit.github.io/nodejs-poolcontroller-api/)
  — protocol-level reference
- [`AquaButler-Server/VISION.md`](https://github.com/ultron-aquabutler/AquaButler-Server/blob/main/VISION.md)
  — full architecture spec

## Status

Content authoring tracked under kanban `t_b2740d21` (Phase 2 wiki content).