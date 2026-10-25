# Troubleshooting

<span class="ab-pill stub">STUB</span>

> **Stub — Phase 2 content.** Canonical troubleshooting procedures in
> `~/AquaButler-Hardware/schematics/RUNBOOK.md` (per gap report Gap 1, Gap 6).

## Field recipes (preview)

- **No comms with pool equipment** — RS-485 adapter validation recipe
  (gap report Gap 1)
- **Cloud won't connect** — WiFi / Ethernet + OpenBalena heartbeat
- **Rotary display blank** — SPI / power / config file
- **"CLOUD UNREACHABLE" banner on the display** — the unit has lost its
  internet connection, but your pool keeps running its schedule and the panel
  still works. See [Cloud Loss Behavior](Cloud-Loss-Behavior.md).
- **Packet capture for issue resolution** — three-method procedure per
  upstream
  [How-to-capture-all-packets-for-issue-resolution](https://github.com/tagyoureit/nodejs-poolController/wiki/How-to-capture-all-packets-for-issue-resolution)
  (gap report Gap 6)

## See Also

- [`AquaButler-Hardware/schematics/RUNBOOK.md`](https://github.com/ultron-aquabutler/AquaButler-Hardware/blob/main/schematics/RUNBOOK.md)
  — full engineering runbook (TBD)
- Upstream [How-to-capture-all-packets-for-issue-resolution](https://github.com/tagyoureit/nodejs-poolController/wiki/How-to-capture-all-packets-for-issue-resolution)
  — packet-capture playbook

## Status

Content authoring tracked under kanban `t_b2740d21` (Phase 2 wiki content).