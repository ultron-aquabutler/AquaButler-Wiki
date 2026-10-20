# njsPC Bridge Integration

<span class="ab-pill stub">STUB</span>

> **Stub — Phase 2 content.** Canonical bridge docs are
> `~/AquaButler-Hardware/docs/Architecture.md` §2 and the gap report Gap 7
> (njsPC-emits-reference, to be authored).

## What the bridge does

AquaButler runs upstream `nodejs-poolController` v10.0.2 as a sidecar on the
CM4 to talk RS-485 to the Pentair OCP. The bridge translates OCP-mediated
protocol traffic to/from our `pool/<customer_id>/...` MQTT topology.

## Architecture (preview)

```
+----------------+   RS-485    +-------------+   MQTT    +-----------------+
| Pentair pool   | <---------> | njsPC       | <-------> | AquaButler     |
| equipment      |             | bridge      |           | core (CM4)     |
| (OCP, pumps,   |             | (sidecar    |           |                 |
|  heaters,      |             |  container) |           |                 |
|  IntelliChem)  |             +-------------+           +-----------------+
+----------------+                                              |
+--> pool/<customer_id>/...
    (AquaButler cloud MQTT)
```

## See Also

- Upstream [Data-Structures.md](https://github.com/tagyoureit/nodejs-poolController/wiki/Data-Structures)
  — emit schema
- Upstream [Configuration.md](https://github.com/tagyoureit/nodejs-poolController/wiki/Configuration)
  — packet framing
- [`AquaButler-Hardware/docs/Architecture.md`](https://github.com/ultron-aquabutler/AquaButler-Hardware/blob/main/docs/Architecture.md)
  §2 — engineering source of truth

## Status

Content authoring tracked under kanban `t_b2740d21` (Phase 2 wiki content) +
`t_5cd77dad` (Gap 8 njsPC-emits-reference).