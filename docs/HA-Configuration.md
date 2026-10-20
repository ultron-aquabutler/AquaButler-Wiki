# Home Assistant Configuration

<div class="ab-pill pilot" markdown="span">BETA v1.0</div>

Connect your AquaButler pool controller to a Home Assistant instance over MQTT. AquaButler publishes its entities automatically — no hand-written `configuration.yaml` block required.

## Before you start

You'll need three things:

1. **Your AquaButler customer ID** — the UUID printed on the inside of the enclosure lid and on your Welcome Card (example: `b3f9a1c4-2e57-4d0f-b91d-12c5e9f9a301`).
2. **Your MQTT broker address and credentials** — these came in the same envelope as your customer ID. If you lost them, request a re-issue from the customer portal under **Settings → MQTT**.
3. **A Home Assistant installation** with the [MQTT integration](https://www.home-assistant.io/integrations/mqtt/) enabled.

!!! tip "Optional: per-area labelling"
    HA will assign every AquaButler entity to the **Backyard** area by default. Once the device appears in HA, drag it to a different area (e.g. *Pool House*) to override the default.

## Quick setup (3 steps)

### 1. Add the MQTT integration to Home Assistant

If this is the first time you've used MQTT in HA, do this once:

1. In HA, go to **Settings → Devices & Services → Integrations**.
2. Search for **MQTT** and click it.
3. Fill in:
    - **Broker:** your AquaButler broker host (from the Welcome Card).
    - **Port:** `8883` (TLS) for production, `1883` for local dev.
    - **Username / password:** the MQTT credentials from your Welcome Card.
    - **Discovery:** check this box. This is what tells HA to listen for the AquaButler device-announce payloads.
4. Click **Submit**. HA connects and listens for the discovery topics.

HA does not need any device-specific `configuration.yaml` block. Skip the "manual MQTT sensor" setup articles — AquaButler is a discovery-first device.

!!! warning "Discovery prefix collision"
    If your HA instance also runs another MQTT device that publishes under `homeassistant/...`, that's fine — every device in HA's discovery protocol uses the same top-level prefix. AquaButler's entities will appear under the device card named **AquaButler Pool &lt;customer-id&gt;**, distinct from your other devices.

### 2. Power-cycle your AquaButler (if not already on)

The MQTT discovery payloads are published by the rotary display firmware once per boot, retained. They reach HA on MQTT connect — no customer action needed beyond the broker configuration in step 1.

If your unit has been running for hours and you want to force a fresh publish, hold the rotary knob > 3 seconds to enter **Service Mode**, then exit it. This triggers a firmware reboot that re-publishes the discovery payloads.

### 3. Verify in Home Assistant

Within ~30 seconds of power-on, the **Devices & Services → MQTT** panel should show a new device card:

> **AquaButler Pool &lt;your customer ID&gt;** — manufacturer *Backyard Butlers*, model *AquaButler v1.0*.

Click into it. You'll see all 13 entities grouped under one device:

| Entity                          | Type           | Notes |
|---------------------------------|----------------|-------|
| Pool pH                         | Sensor         | Water pH reading |
| Pool ORP                        | Sensor         | Sanitizer ORP (mV) |
| Pool Temperature                | Sensor         | Water temperature (°F) |
| Ambient Temperature             | Sensor         | Air temperature (°F) |
| Pump RPM                        | Sensor         | Variable-speed pump feedback (diagnostic) |
| Errors (24h)                    | Sensor         | Error count last 24h (diagnostic) |
| Pump Run Hours                  | Sensor         | Total pump runtime (diagnostic) |
| WiFi Signal                     | Sensor         | RSSI in dBm (diagnostic; disabled by default — enable in entity settings) |
| Pump Running                    | Binary Sensor  | On when pump is active |
| Freeze Protection               | Binary Sensor  | On when freeze protection is engaged |
| Pool Pump                       | Switch         | Toggle pump on/off |
| Filter Cycle                    | Switch         | Trigger a filter cycle |
| Heater Setpoint                 | Number         | Set target temperature (60..104 °F) |

If the device card doesn't appear:

- Wait another 30 seconds (HA polls retained messages on a timer).
- Verify the broker connection is green in HA's MQTT integration.
- Verify your credentials grant `read` access to `homeassistant/#` — AquaButler's per-customer ACL grants this by default; check with your installer.

## Command authority — last write wins

AquaButler accepts control commands from **both** Home Assistant and the AquaButler customer portal, written to the same canonical MQTT topics. HA command publishes and portal command publishes compete via **last-write-wins** at the broker.

What this means in practice:

- If HA is mid-toggling the heater and you adjust the setpoint in the portal, the most recent action takes effect. The other one is overridden.
- You will not see a "command rejected" error if both UI surfaces are open at the same time — the broker silently arbitrates.
- For deterministic control, **use one surface at a time**. The rotary display on the enclosure stays in sync regardless (it mirrors the canonical state from the firmware's MQTT subscriptions).

!!! info "Safety interlocks still apply"
    Every command goes through the same safety checks regardless of source (rotary, portal, HA, or cloud). Commands outside the published range (e.g. heater setpoint above 104 °F, chlorination duration over 10 minutes) are rejected by the AquaButler controller and logged to the audit trail. HA does not bypass these limits.

## Disabling discovery

Discovery is **opt-in** in the AquaButler customer portal under **Settings → Integrations → Home Assistant**. Toggle **Enable MQTT auto-discovery** off and the rotary firmware stops publishing retained discovery payloads at the next boot. Existing HA entities remain visible until you remove them from HA, but the firmware no longer refreshes them on reconnect.

To re-enable, toggle it back on and reboot the firmware (or wait for the next nightly reboot if the customer's installer scheduled one).

## What gets published (technical detail)

For each customer, the firmware publishes exactly 13 retained payloads under the topic tree:

```
homeassistant/<component>/<node_id>/<object_id>/config
```

where `<node_id>` is `aquabutler_<customer-id>` — every entity shares the same device card.

**Full topic list:**

```
homeassistant/aquabutler_<id>/sensor/ph/config
homeassistant/aquabutler_<id>/sensor/orp/config
homeassistant/aquabutler_<id>/sensor/temp_pool/config
homeassistant/aquabutler_<id>/sensor/temp_air/config
homeassistant/aquabutler_<id>/sensor/pump_rpm/config
homeassistant/aquabitler_<id>/sensor/errors_24h/config
homeassistant/aquabutler_<id>/sensor/run_hours/config
homeassistant/aquabutler_<id>/sensor/rssi/config
homeassistant/aquabutler_<id>/binary_sensor/pump_state/config
homeassistant/aquabutler_<id>/binary_sensor/freeze_protection/config
homeassistant/aquabutler_<id>/switch/pump/config
homeassistant/aquabutler_<id>/switch/filter/config
homeassistant/aquabutler_<id>/number/heater_setpoint/config
```

Topic prefixes are deliberately reserved under the per-customer ACL. The firmware publishes these topics with its existing device-bound MQTT credential — no additional credential setup is needed.

## Troubleshooting

### Device card is missing or shows "Unavailable"

1. Confirm the MQTT integration is green in HA.
2. Check the firmware version: **Settings → About** in the AquaButler portal should report `Rotary firmware 0.1.0` or later. Earlier firmware versions predate the auto-discovery feature.
3. Force a fresh publish: enter and exit Service Mode on the rotary display.
4. If it still doesn't appear, check the broker is allowing retained messages. Some brokers strip retained messages from clients without the `retain` flag in their ACL — the AquaButler broker config grants retain by default; if you're using a third-party broker, verify the credential permission.

### Entities appear but show "Unknown" state

The state topics are reading but the values haven't been published yet. Wait 60 seconds — telemetry publishes at 1 Hz and state initializes within the first poll. If still Unknown after a minute, the firmware has not connected to MQTT.

### Command entities (Pump, Filter, Heater Setpoint) won't respond

The most common cause is the rotator firmware's safety check rejecting the command. Check **Settings → Activity Log** in the portal for audit entries with `outcome: "rejected_safety"` and the matching `error` string. The HA command is logged with `source: "home_assistant"` so it's distinguishable from rotary-portal commands.

### Dual-controllers confused (HA + portal)

You toggled the heater in HA to 82 °F but the rotary display shows 80 °F. The portal updated the setpoint *after* your HA click — last-write-wins. Pick one surface, complete the action, and the other will catch up on next state poll.

## See Also

- [**MQTT Bindings**](MQTT-Bindings.md) — the underlying topic schema, including the `homeassistant/` reserved prefix and ACL config
- [**Troubleshooting**](Troubleshooting.md) — when the device card never appears, or commands silently fail
- [**Customer Portal**](Customer-Portal.md) — the alternative control surface (and where you toggle discovery off)
- **AquaButler engineering source of truth:** [`docs/wiki/mqtt-topic-schema.md`](https://github.com/ultron-aquabutler/AquaButler-Server/blob/main/docs/wiki/mqtt-topic-schema.md) § HA MQTT auto-discovery
- **HA MQTT discovery spec:** https://www.home-assistant.io/integrations/mqtt/#mqtt-discovery

## Status

Authored 2026-10-20 per Bryan's decision on kanban `t_d1875bc5` (option B: in Beta v1.0). Payload format locked in `src/_shared/ha_discovery.py`; per-customer ACL widened in `docs/wiki/mqtt-topic-schema.md` §Per-customer ACL specification ACL-B. Beta-tested on the first 10 customer units starting 2026-10-22 — feedback rounds close 2026-11-05.
