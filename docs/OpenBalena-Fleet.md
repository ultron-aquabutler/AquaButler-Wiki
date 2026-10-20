# OpenBalena Fleet

<span class="ab-pill stub">STUB</span>

> **Stub — Phase 2 content.** No wiki-source-of-truth defined yet; canonical
> docs are the AquaButler-Server `fleet/` directory.

## What it does

Container OTA, fleet health, per-customer device identity provisioning.

- **Per-device identity** — every customer unit gets a unique OpenBalena
  UUID at provisioning; that UUID is the source of truth for the cloud-side
  per-customer MQTT namespacing.
- **OTA updates** — AquaButler core containers update independently of the
  carrier firmware. Container images are tagged by semantic version; the
  fleet rolls forward in waves.
- **Health heartbeats** — every unit reports heartbeat + last-seen to the
  OpenBalena supervisor; missing heartbeats trigger alert workflows.

## See Also

- [`AquaButler-Server/fleet/`](https://github.com/ultron-aquabutler/AquaButler-Server/tree/main/fleet)
  — fleet management stack
- [OpenBalena upstream](https://www.balena.io/docs/reference/OpenBalena/introduction/)
  — protocol-level reference

## Status

Content authoring tracked under kanban `t_b2740d21` (Phase 2 wiki content).