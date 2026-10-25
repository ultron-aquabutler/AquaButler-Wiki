# What Happens When Your AquaButler Loses Internet

<span class="ab-pill pilot">CUSTOMER GUIDE</span>

> **Your pool keeps running.** Losing your internet connection does **not** stop
> your AquaButler, your schedules, or your panel. You may see a notice on the
> display and a note in the customer portal, but your pool carries on exactly
> as it was programmed to.

This page explains what actually happens, what you'll see, and what you can
still do while the connection is down.

---

## The short version

| | |
|---|---|
| **Does my pool stop?** | No. Your schedules keep running. |
| **Can I still control it from the panel?** | Yes. Everything works. |
| **Will I get an alarm?** | Only a calm notice — not a fault. |
| **Do I need to do anything?** | Usually not. Just fix the connection when you can. |

---

## What you'll see

### On your rotary display

A **red banner** appears along the bottom of the status screen reading
`CLOUD UNREACHABLE`.

The banner sits at the bottom of the screen, so it never covers the readings
you care about — your pH, ORP, and pump state stay fully visible.

The banner is **persistent**, not a blinking alert. It stays until either:

- your connection comes back, or
- you dismiss it (see [Dismissing the banner](#dismissing-the-banner)).

Press and hold the knob to open the detail screen, which shows you the
connection state and confirms that everything is still running.

### In the customer portal

Your pool appears with a **warning** — not an error, and not a service
request. It reads along the lines of:

> Offline — your pool is still running its schedule and the panel still works.

That warning is informational. It tells you that the portal can't reach your
unit right now, not that something has gone wrong with your pool.

---

## What still works

Everything local. Your AquaButler talks to your pool equipment over a
local connection that has nothing to do with the internet.

- ✅ **Your schedules keep running.** Filtration, chlorination, and heating
  continue on the schedule you set. There is no time limit on this — your
  AquaButler will keep running your schedules for as long as the power is on.
- ✅ **The panel works.** You can still run the pump, start a filter cycle,
  override chlorination, and change the heater setpoint from the rotary
  display, whether or not you have internet.
- ✅ **Your pool equipment keeps working.** The AquaButler and your pool
  equipment communicate locally, exactly as they do when the connection is
  healthy.
- ✅ **Safety features keep working.** Freeze protection, the chlorine
  lockout, and the service-mode timeouts all behave identically.

---

## The one exception: Service mode

If **someone physically opens the unit and puts it into service mode** — by
entering the installer PIN on the display — schedules may be paused while
they work. That is intentional: a technician working on the equipment needs
it to hold still.

Everything else is unaffected.

---

## Why the display warns you at all

If the display said nothing, a silent outage would be hard to spot. Your
AquaButler might quietly stop reporting to the portal for a week, and by the
time you noticed, the details would be stale.

The notice means: *"your pool is fine, but I can't reach the internet right
now, so anything you do out in the cloud isn't getting through."*

That distinction matters — it's the difference between "your pool needs
attention" and "your pool is fine, the phone line is down."

---

## Dismissing the banner

If the banner is in your way while you're working at the unit:

1. Turn the knob until you're on the cloud notice page (the third page of
   the status screen), **or** press and hold the knob to open the cloud
   detail screen.
2. Press the button to dismiss it.

The banner stays dismissed until the situation changes. If a *new* problem
appears later — a different kind of disconnection — the banner comes back on
its own, so you won't miss it.

---

## Common causes and quick fixes

| What happened | What to check |
|---|---|
| Your home internet is down | Check your router and whether other devices are online. Your pool is unaffected in the meantime. |
| Your WiFi dropped out | The AquaButler retries on its own. Check the signal strength on the display (status page 2, `RSSI`). |
| The unit lost power briefly | The unit reboots and reconnects by itself. It may take a minute or two. |
| A network cable was unplugged | Plug it back in. The display shows `CLOUD LINK: UP` once it reconnects. |
| Your network is up but nothing changed | Give it a minute to retry, then power-cycle the unit if needed. |

**If your display is showing `SERVICE MODE` instead** — a technician has put
the unit into service mode. That is normal during a service visit, and it is
not an error. **If you did not expect it**, contact your installer.

**If your display is showing `COMMISSIONING`** — the unit is being installed
or set up. This is expected during installation and is never treated as a
fault.

---

## What to do when the connection comes back

Nothing. The AquaButler reconnects on its own and clears the banner by
itself. Your customer portal goes back to normal as soon as the connection
is re-established — no restart, no reset, no reconfiguration.

---

## Technical reference

For developers and installers:

| Item | Value |
|---|---|
| MQTT topic | `pool/<id>/status/degraded` |
| QoS | 0 |
| Retained | **Yes** — the last known state survives a disconnect |
| Values | `ok` \| `cloud_unreachable` \| `service_mode` \| `commissioning_offline` |

Full specification:
[`mqtt-topic-schema.md` §Amendment 2026-10-25](https://github.com/ultron-aquabutler/AquaButler-Server/blob/main/docs/wiki/mqtt-topic-schema.md#amendment-2026-10-25--poolidstatusdegraded)

Locked display strings:
[`canonical-messages.md` §Cloud-loss degraded status](https://github.com/ultron-aquabutler/AquaButler-Server/blob/main/docs/wiki/canonical-messages.md#cloud-loss-degraded-status-rotary-display--portal)

---

## See Also

- [Rotary Display](Rotary-Display.md) — the display's modes and color coding
- [Troubleshooting](Troubleshooting.md) — general field procedures
- [Customer Portal](Customer-Portal.md) — what the portal shows
- [MQTT Bindings](MQTT-Bindings.md) — the full topic reference
