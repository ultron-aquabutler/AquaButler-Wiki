# AquaButler Wiki

> Production-grade pool automation on Raspberry Pi CM4. Ships in an IP65/IP67
> enclosure, talks RS-485 to your Pentair gear, MQTTs to the AquaButler cloud.

---

## What is AquaButler?

AquaButler is a turnkey hardware + cloud stack that puts a modern, secure
automation layer between your pool equipment and the AquaButler mobile /
web portal. We run on your equipment pad, not in your data center.

- **Compute:** CM4 extended-temperature, hardened carrier board
- **Bus interface:** dual isolated RS-485 (MAX3485 + ADM2587E)
- **Relay stack:** Sequent HATs (relays + ADC + chemistry probe front-end)
- **Cloud:** OpenBalena fleet management + Supabase auth + per-customer MQTT
- **UI:** optional wall-mounted rotary display + customer web portal

---

## Getting Started

| | |
|---|---|
| **[Hardware Overview](Hardware-Overview.md)** | What's in the box, what's on the board, what each connector does |
| **[Getting Started](Getting-Started.md)** | Mount the enclosure, connect power + RS-485 + WiFi, register in the cloud portal |

## Software & Protocols

| | |
|---|---|
| **[MQTT Bindings](MQTT-Bindings.md)** | Every topic your installation publishes/subscribes to (`pool/<customer_id>/...`) |
| **[njsPC Bridge Integration](njsPC-Bridge-Integration.md)** | How AquaButler talks to the upstream nodejs-poolController bridge for Pentair protocol support |

## Cloud & Fleet

| | |
|---|---|
| **[OpenBalena Fleet](OpenBalena-Fleet.md)** | Container OTA, fleet health, per-customer device identity |
| **[Customer Portal](Customer-Portal.md)** | Per-customer identity, JWT, audit log, mobile + web surfaces |

## Hardware Reference

| | |
|---|---|
| **[Rotary Display](Rotary-Display.md)** | The optional 240×240 SPI panel — service-mode / manual-mode / status-mode strings |

## Operations

| | |
|---|---|
| **[Cloud Loss Behavior](Cloud-Loss-Behavior.md)** | What your pool does when the internet drops — schedules keep running, the panel keeps working |
| **[Troubleshooting](Troubleshooting.md)** | Field recipes for "no comms," "cloud won't connect," "rotary display blank" |
| **[API Reference](API-Reference.md)** | HTTP + MQTT surface for integrators and partners |

---

## Project & Repositories

| Project | Description |
|---------|-------------|
| [AquaButler-Hardware](https://github.com/ultron-aquabutler/AquaButler-Hardware) | Carrier board, schematics, BOM, enclosure, engineering source of truth |
| [AquaButler-Server](https://github.com/ultron-aquabutler/AquaButler-Server) | Cloud side: Supabase, MQTT broker, per-customer portal, rotary-display firmware |
| [Controller-dashPanel](https://github.com/ultron-aquabutler/Controller-dashPanel) | UI theme — AquaButler branding over upstream nodejs-poolcontroller-dashPanel |

## Supported Equipment

AquaButler communicates with these Pentair systems via RS-485:

- **IntelliCenter** (all models, including v3.008 firmware)
- **EasyTouch**
- **IntelliTouch** (including i9+3 expansion)
- **SunTouch** (status/control only)
- **AquaLink** (via Aqualinkd bridge — status/control only)

Powered by upstream `nodejs-poolController` v10.0.2.

---

## See Also

- **Upstream wiki:** [tagyoureit/nodejs-poolController/wiki](https://github.com/tagyoureit/nodejs-poolController/wiki) — referenced for protocol-level documentation
- **Upstream APIs:** [nodejs-poolcontroller-api](https://tagyoureit.github.io/nodejs-poolcontroller-api/) — Swagger
- **Source repo docs:** [`AquaButler-Hardware/docs/Architecture.md`](https://github.com/ultron-aquabutler/AquaButler-Hardware/blob/main/docs/Architecture.md) — engineering source of truth

---

*AquaButler™ — Backyard Butlers LLC.*