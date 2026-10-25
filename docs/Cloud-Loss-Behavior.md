# What Happens When Your AquaButler Loses Internet

<div class="ab-pill pilot" markdown="span">BETA v1.0</div>

Your AquaButler keeps working when it loses its internet connection.

**Your pool keeps running its schedule.** Filter and pump schedules do not stop,
and they do not have a time limit — they keep running until the connection comes
back, no matter how long that takes.

**Your panel keeps working.** The rotary display stays fully interactive. You
can still run pumps, change chemistry, and put the controller into service mode
exactly as you would normally.

The only thing you lose is the ability to see and change things **from the
customer portal or your phone** — the cloud connection is what carries those.

---

## What you will see

### On the rotary display

A colored banner appears along the bottom of the status page. It stays there
until the connection is restored, so it never flashes and disappears before you
have read it.

| Banner | Color | What it means |
|---|---|---|
| `CLOUD UNREACHABLE` | Red | The AquaButler has lost its internet connection. Your schedule is still running and the panel still works. |
| `SERVICE MODE` | Orange | A technician has put the controller into service mode. This is a normal state during a service visit. |
| `COMMISSIONING` | Yellow | An installer is setting up the unit. This is **not** a fault. |

Rotate to the third status page to read the details. It will confirm the two
things that matter:

- `SCHEDULE STILL RUNNING`
- `LOCAL CONTROL AVAILABLE`

Long-press from the status page to open the full `CLOUD ALERT` screen, which
also shows the exact state and whether the link is currently up or down.

### In the customer portal

The portal shows one of four states:

| Portal state | What you see |
|---|---|
| Healthy | Normal — no message. |
| Offline | **Warning** — "Offline — your pool is still running its schedule and the panel still works." |
| In service mode | **Info** — "In service mode." with the reason and the time it started. |
| Commissioning | **Neutral** — "Commissioning — not a fault." |

Note the wording difference on purpose. An offline AquaButler is a **warning,
not an alarm** — nothing has stopped, and nothing needs your attention right
away.

---

## The one exception: service mode

Service mode is the only situation where schedules may pause.

If someone at the unit (or in the portal) puts the controller into **service
mode**, schedule execution can be interrupted — that is the point of service
mode, so a technician can work on the unit safely.

Everything else keeps running. A lost connection by itself never stops a
schedule.

---

## Why the alert is dismissible

A technician working on a pool should not have to dismiss a banner over and
over.

Press to dismiss and the banner clears. It stays dismissed until the state
actually changes — so if the unit goes offline a second time, the banner comes
back. Dismissing it never hides a *new* problem.

---

## Frequently asked

**Does losing internet damage anything?**
No. The connection loss is detected and handled by the controller itself. The
last known state is recorded so the portal can tell the difference between
"this unit just went offline" and "this unit has been offline for a while."

**Will my schedule be stale or wrong when the connection comes back?**
No. Schedules are stored on the controller, not in the cloud. Nothing about a
schedule depends on the internet connection, and nothing is silently truncated
while the connection is down.

**The panel says `COMMISSIONING` — is something broken?**
No. Commissioning means an installer intentionally took the unit offline as
part of setup. It is deliberately shown as neutral rather than as a fault so
it never triggers an alarming notification.

**Can I tell the difference between "offline" and "in service mode"?**
Yes. They are separate banners with separate colors, and the detail screen
reports the exact state.

---

## For installers and technicians

The degraded state is published on MQTT at `pool/<id>/status/degraded`, **retained**
(QoS 0), so the broker holds the last known value even after the device
disconnects:

| Value | Meaning |
|---|---|
| `ok` | Cloud reachable, nothing degraded. |
| `cloud_unreachable` | Lost cloud connectivity. Schedule running, local control available. |
| `service_mode` | A local control action put the unit into service mode. |
| `commissioning_offline` | Installer intentionally took the unit offline. Not a fault. |

Because the value is retained, a unit that loses power or drops off the network
abruptly still leaves a readable last-known state at the broker — the portal
combines that with the broker's own connection-drop event to decide what to
show.

Service-mode transitions are written to the audit stream (`pool/<id>/audit/<stream>`)
with the source (local, cloud, or auto-timeout), the reason, and a timestamp.
Service mode is the one thing that can stop a customer's schedule, so it is
always auditable.

The full topic contract is in the
[MQTT schema](https://github.com/ultron-aquabutler/AquaButler-Server/blob/main/docs/wiki/mqtt-topic-schema.md)
(amended 2026-10-25) and the display strings are in
[Canonical Messages](https://github.com/ultron-aquabutler/AquaButler-Server/blob/main/docs/wiki/canonical-messages.md).

## See Also

- [Troubleshooting](Troubleshooting.md) — field recipes
- [Rotary Display](Rotary-Display.md) — display hardware and modes
- [Customer Portal](Customer-Portal.md) — portal behavior
- [MQTT Bindings](MQTT-Bindings.md) — topic reference for integrators
