# Home Assistant Automation Audit
**Generated:** 2026-04-25  
**Total automations:** 49 (45 enabled, 4 disabled)

---

## Summary

| Category | Count |
|----------|-------|
| Active (triggered today) | 21 |
| Redundant duplicates | 6 (3 pairs) |
| Stale — never triggered | 4 |
| Stale — >90 days (enabled) | 11 |
| Intentionally disabled | 4 |
| Borderline 8–90 days | 3 |

**Recommended deletions:** 8  
**Recommended merges:** 1  
**Recommended investigations:** 4

---

## 🔴 REDUNDANT — Delete or Merge

### Entry Door Lights (duplicate pair)
| Entity | Friendly Name | State | Last Triggered |
|--------|--------------|-------|----------------|
| `automation.entry_door_lights` | Entry Door Lights | on | 162d ago (2025-11-14) |
| `automation.entryway_door_light` | Entryway Door Light | on | **Today** |

**Verdict: DELETE `automation.entry_door_lights`.**  
Same purpose, same room. The `entryway_door_light` is clearly the active one — triggered daily. The `entry_door_lights` hasn't fired in 162 days and is likely a renamed predecessor.

---

### Goodnight Lock Front Door (duplicate pair)
| Entity | Friendly Name | State | Last Triggered |
|--------|--------------|-------|----------------|
| `automation.goodnight_lock_front_door` | Goodnight - Lock Front Door | on | Today |
| `automation.lock_front_door_on_goodnight` | Lock Front Door on Goodnight | on | Today |

**Verdict: INVESTIGATE then DELETE one.**  
Both active, both triggered today, both lock the front door on goodnight. Highly likely these are the same automation created twice. Open both in the HA editor, confirm they have identical triggers/conditions/actions, then delete the one with the less-clean entity ID (`automation.lock_front_door_on_goodnight`).

---

### Plant 1 Has Enough Water (duplicate pair)
| Entity | Friendly Name | State | Last Triggered |
|--------|--------------|-------|----------------|
| `automation.plant_has_enough_water` | Plant 1 Has Enough Water | on | **Never** |
| `automation.plant_1_has_enough_water` | Plant 1 has enough water | on | 485d ago (2024-12-26) |

**Verdict: DELETE both or consolidate into one working automation.**  
Neither has fired in over a year. `plant_has_enough_water` has never triggered at all. These are almost certainly duplicates of each other. If plant monitoring is still wanted, delete both and recreate clean. If not, delete both.

---

### Plant 1 Needs Water (duplicate pair — same friendly name!)
| Entity | Friendly Name | State | Last Triggered |
|--------|--------------|-------|----------------|
| `automation.plant_1_needs_water` | Plant 1 needs water | on | 484d ago (2024-12-26) |
| `automation.plant_1_needs_water_2` | Plant 1 needs water | on | 370d ago (2025-04-20) |

**Verdict: DELETE `automation.plant_1_needs_water` (older, longer stale).**  
Identical friendly names — this is a copy that was made and never cleaned up. `_2` is slightly less stale (370 vs 484 days). Neither is healthy. If plant automation is wanted, keep `_2` and fix it; if not, delete both.

---

## 🟡 STALE — Never Triggered (Enabled)

| Entity | Friendly Name | Recommendation |
|--------|--------------|----------------|
| `automation.livingroom_ceiling_fan` | LivingRoom Ceiling Fan | **DELETE** — Never triggered, no evidence this has ever worked. Ceiling fan likely controlled manually or via a different path. |
| `automation.restart_living_room_sensor` | Restart Living room Sensor | **INVESTIGATE** — Never triggered. Kitchen/Office sensor restarts fire regularly; this one never has. Either the living room sensor never fails or the trigger is broken. Check trigger entity. |
| `automation.epone_master_bathroom_restart` | EPOne Master bathroom Restart | **INVESTIGATE** — Never triggered. May be misconfigured. The EP One in master bathroom is a smart plug, not a presence sensor — confirm this automation's target device is correct. |
| `automation.plant_has_enough_water` | Plant 1 Has Enough Water | **DELETE** — See redundant pair above. |

---

## 🟡 STALE — >90 Days (Enabled)

| Entity | Friendly Name | Last Triggered | Recommendation |
|--------|--------------|----------------|----------------|
| `automation.play_worship_sleep_on_home_pod_minis` | Play Worship Sleep on Home Pod Minis | 504d ago (2024-12-07) | **DELETE** — 1.4 years stale. HomePod integration likely broken or habit changed. |
| `automation.lets_play_a_video_game` | Let's play a video game | 501d ago (2024-12-09) | **DELETE** — 1.4 years stale. Scene/routine no longer in use. |
| `automation.garage_door_opens_when_lisa_or_nathan_enter_the_home_zone` | Garage door opens when… | 471d ago (2025-01-09) | **DISABLED — KEEP DISABLED.** Per CLAUDE.md: safety concern. Intentionally off. Consider deleting if you're certain this will never be re-enabled. |
| `automation.plant_1_has_enough_water` | Plant 1 has enough water | 485d ago (2024-12-26) | **DELETE** — See redundant pair above. |
| `automation.plant_1_needs_water` | Plant 1 needs water | 484d ago (2024-12-26) | **DELETE** — See redundant pair above. |
| `automation.plant_2_needs_water` | Plant 2 Needs Water | 460d ago (2025-01-20) | **DELETE** — Plant 2 monitoring has been dead for 1.3 years. |
| `automation.plant_1_needs_water_2` | Plant 1 needs water | 370d ago (2025-04-20) | **DELETE** (or fix) — See redundant pair above. |
| `automation.restart_kitchen_sensor` | Restart Kitchen Sensor | 250d ago (2025-08-18) | **KEEP** — Restart watchdog. 250 days means the kitchen sensor has been stable, not that the automation is broken. |
| `automation.restart_internet` | Restart Internet | 217d ago (2025-09-19) | **KEEP** — Same logic. Internet stability = no triggers. |
| `automation.office_fan_in_if_too_hot` | Office fan on if too hot | 157d ago (2025-11-18) | **KEEP (seasonal)** — Last triggered in November. Office hasn't been hot enough since. Expect this to fire again in summer. |
| `automation.empty_house_living_room_lights_on` | Empty House - Living room lights on | 124d ago (2025-12-22) | **INVESTIGATE** — 124 days without the house being empty? Either presence detection is stuck, or this was disabled indirectly. Verify `person.nathan_veer` and `person.lisa` presence tracking is working. |
| `automation.entry_door_lights` | Entry Door Lights | 162d ago (2025-11-14) | **DELETE** — See redundant pair above. |

---

## 🔵 INTENTIONALLY DISABLED — Keep as-is

Per CLAUDE.md — do not re-enable without deliberate decision:

| Entity | Friendly Name | Last Triggered | Note |
|--------|--------------|----------------|------|
| `automation.garage_door_opens_when_lisa_or_nathan_enter_the_home_zone` | Garage door opens when… | 471d ago | Safety concern |
| `automation.modem_power_cycle` | Modem Power Cycle | Never | Intentionally disabled |
| `automation.nathans_night_off` | Nathan's Night Off | 490d ago | Intentionally disabled |
| `automation.turn_off_master_bedroom_ceiling_fan_after_1_hour` | Turn Off Master Bedroom Ceiling Fan | 350d ago | Intentionally disabled |

---

## 🟡 BORDERLINE — Monitor

| Entity | Friendly Name | Last Triggered | Note |
|--------|--------------|----------------|------|
| `automation.master_hallway_lights_nighttime` | Master Hallway Lights Nighttime | 10d ago (2026-04-15) | Fine — nighttime only, seasonal variation expected. |
| `automation.restart_scarlett_audio_interface` | Restart Speakers and Scarlett | 82d ago (2026-02-01) | Fine — only fires when device crashes. |
| `automation.mailbox_notification` | Notifications (mailbox) | 34d ago (2026-03-21) | Fine — depends on mailbox activity. |

---

## ✅ ACTIVE — No Action Needed

Triggered today (2026-04-25):

- Driveway Lights On at sunset / Off at sunrise
- Dwayne's Air Purifier On/Off Times
- Entryway Door Light
- Garage Lights
- Goodnight - Lock Front Door *(see duplicate note above)*
- Kitchen Lights - Day Time / Night Time
- Laundry Room Lights
- Living Room Lights / Air Purifier 2
- Lock Front Door on Goodnight *(see duplicate note above)*
- Master Bath Off - Both In Bed
- Master Bathroom Lights / Humidity
- Master Bedroom Lights / Master Bedroom Lights (Sensor 2) *(intentional dual-sensor architecture)*
- Master Hallway Lights
- Nathan's bed set to Zero G at night
- Office CO2 Levels - Turn on Nest Fan
- Office Lights / Office Lights Watchdog / Office fan off when cool enough
- Outside Walkway Lights-f
- Presence sensors offline
- Restart Home Assistant / Restart Office Sensor
- Turn off master toilet fan after 30 min

---

## Action Checklist

```
DELETE (8 automations):
[ ] automation.entry_door_lights           — duplicate of entryway_door_light (162d stale)
[ ] automation.plant_has_enough_water      — never triggered, duplicate
[ ] automation.plant_1_has_enough_water    — 485d stale, duplicate
[ ] automation.plant_1_needs_water         — 484d stale, duplicate of _2
[ ] automation.plant_2_needs_water         — 460d stale, no longer monitored
[ ] automation.lets_play_a_video_game      — 501d stale, unused scene
[ ] automation.play_worship_sleep_on_home_pod_minis  — 504d stale
[ ] automation.livingroom_ceiling_fan      — never triggered

MERGE/DEDUPE (1):
[ ] automation.lock_front_door_on_goodnight  — confirm identical to goodnight_lock_front_door, then delete

INVESTIGATE (4):
[ ] automation.empty_house_living_room_lights_on  — 124d stale, check presence tracking
[ ] automation.restart_living_room_sensor          — never triggered, check trigger config
[ ] automation.epone_master_bathroom_restart       — never triggered, check target device
[ ] automation.plant_1_needs_water_2               — 370d stale, fix or delete

KEEP DISABLED — no change:
[ ] automation.garage_door_opens_when_*    — safety concern
[ ] automation.modem_power_cycle           — intentional
[ ] automation.nathans_night_off           — intentional
[ ] automation.turn_off_master_bedroom_ceiling_fan_after_1_hour  — intentional
```
