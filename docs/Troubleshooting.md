# Troubleshooting

<span class="ab-pill stub">STUB</span>

> **Stub — Phase 2 content.** Canonical troubleshooting procedures in
> `~/AquaButler-Hardware/schematics/RUNBOOK.md` (per gap report Gap 1, Gap 6).

## Field recipes (preview)

- **No comms with pool equipment** — RS-485 adapter validation recipe
  (gap report Gap 1)
- **Cloud won't connect** — WiFi / Ethernet + OpenBalena heartbeat
- **Rotary display blank** — SPI / power / config file
- **Pool is running but the portal shows it offline** — see
  [Losing Internet Connection](Losing-Internet-Connection.md). The pool is
  almost certainly fine; the display's `CLOUD UNREACHABLE` banner means the
  cloud link is down, not that the controller has failed.
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