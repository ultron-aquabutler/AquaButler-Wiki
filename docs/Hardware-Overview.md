# Hardware Overview

> Source of truth for the AquaButler v1 carrier + enclosure stack. Paraphrases
> the upstream njsPC wiki's hardware model adapted for our IP65/IP67 pad-mount
> form factor. **NOT** an engineering specification — that lives in
> [`AquaButler-Hardware/docs/Architecture.md`](https://github.com/ultron-aquabutler/AquaButler-Hardware/blob/main/docs/Architecture.md)
> (the canonical engineering doc). This page is the customer + installer surface.

---

## What's in the box

- AquaButler enclosure (polycarbonate, IP65/IP67) with ePTFE vent
- CM4 carrier board (industrial temp, +80°C ceiling)
- Sequent HAT stack: Watchdog + Relay + ADC
- Sequent Super Watchdog HAT (battery-backed, supercapacitor option)
- 5V/3A regulated supply with surge protection
- M12 RS-485 gland + outdoor shielded twisted pair cable (10 m, more on request)
- RP-SMA WiFi antenna (or Ethernet gland alt)
- Cable kit, gland nuts, mounting template

## What's on the board

```
+----------------------------------------------------------+
|  Enclosure (polycarbonate, IP65/IP67)                    |
|                                                          |
|  +------ Carrier PCB (the product) -----+                |
|  |  RPi CM4 ext-temp SoM               |                |
|  |     |                                |                |
|  |  Sequent Watchdog HAT (battery side up)|              |
|  |  Sequent Relay HAT (8-relay, 3-IND)  |               |
|  |  Sequent ADC HAT (16-bit, 4-channel) |               |
|  |  Dual isolated RS-485 (MAX3485 + ADM2587E)            |
|  |  Universal-input PSU stage (Mean Well HDR-60-5)        |
|  +----------------------------------------+              |
|                                                          |
|  M12 RS-485 to pool      IEC C13 AC        RP-SMA WiFi   |
+----------------------------------------------------------+
       ePTFE vent plug
```

## Connector map (customer-facing)

| Label | Function | Connector |
|-------|----------|-----------|
| AC IN | 85-264 VAC (auto-sensing) | IEC C13 or hardwired whip |
| RS-485 OUT | Pentair pool bus | IP67 M12 A-coded, 4-pin |
| WiFi ANT | WiFi/BLE antenna | RP-SMA bulkhead |
| ETH (alt) | Wired network option | IP67 RJ45 bulkhead |

## Compute choice (CM4 + custom carrier)

| Spec | Pi 5 | CM4 ext-temp | Pick |
|------|------|--------------|------|
| Max ambient | +50°C | +80°C | CM4 |
| Typical draw | 5V/3A peak | 5V/1.5A | CM4 |
| Heat in sealed box | ~10W worst | ~5W typical | CM4 |
| Longevity (2026→2036) | yes | yes (industrial) | CM4 |

The CM4 + custom-carrier choice is what unlocks the IP65/IP67 + 7-year
lifecycle story. Pi 5 would force active cooling (fan, vent, dust filter
maintenance) — not viable in a customer-installable outdoor unit.

## Bus addressing (per upstream Pentair)

| Address | Subsystem |
|---------|-----------|
| 15 | Broadcast (always) |
| 16 | OCP (Outdoor Control Panel) |
| 32 | Wired controller (Pentair) |
| 33 | njsPC bridge (configurable) |
| 96-111 | Pumps 1-16 |
| 144 | IntelliChem |

Chlorinator uses an alternate packet framing (`16,2,...,16,3`) — see upstream
`Chlorinator.md` and the Engineering Reference in this wiki's API-Reference
section.

## Universal PSU — no field setting needed

The Mean Well HDR-60-5 auto-senses 85-264 VAC. No voltage selector switch, no
jumper. Ship the same unit to 115V and 230V customers.

- **115V site:** connects to one hot leg + neutral (L1 + N)
- **230V site:** connects to both hot legs (L1 + L2); neutral unused

Wiring details per the install manual.

---

## See Also

- [`AquaButler-Hardware/docs/Architecture.md`](https://github.com/ultron-aquabutler/AquaButler-Hardware/blob/main/docs/Architecture.md)
  — full engineering specification, schematics, BOM
- [`AquaButler-Hardware/schematics/`](https://github.com/ultron-aquabutler/AquaButler-Hardware/tree/main/schematics)
  — KiCad files, Gerbers, build sheets
- [`AquaButler-Hardware/bom/aquabutler-carrier-v1-bom.csv`](https://github.com/ultron-aquabutler/AquaButler-Hardware/blob/main/bom/aquabutler-carrier-v1-bom.csv)
  — Bill of Materials
- [`AquaButler-Hardware/enclosure/`](https://github.com/ultron-aquabutler/AquaButler-Hardware/tree/main/enclosure)
  — enclosure drawings, thermal analysis
- Upstream wiki for protocol-level reference:
  [RS-485-Adapter-Details](https://github.com/tagyoureit/nodejs-poolController/wiki/RS-485-Adapter-Details)