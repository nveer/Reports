# Session: Automation Cleanup — Deletions, Merge, Plant Fix
**Date:** 2026-04-25

## Problem
49 automations, several redundant or stale. Nathan approved cleanup after full audit.

## Changes Made

### Deleted (7 automations)
| Automation | Reason |
|-----------|--------|
| `automation.entry_door_lights` | Duplicate of `entryway_door_light` — 162 days stale |
| `automation.livingroom_ceiling_fan` | Never triggered once |
| `automation.lets_play_a_video_game` | 501 days stale, unused scene |
| `automation.play_worship_sleep_on_home_pod_minis` | 504 days stale, HomePod routine abandoned |
| `automation.empty_house_living_room_lights_on` | 124 days stale, presence detection issue |
| `automation.epone_master_bathroom_restart` | Never triggered, wrong target device |
| `automation.goodnight_lock_front_door` | Duplicate of `lock_front_door_on_goodnight` — used fragile event-based trigger |

### Kept (door lock merge)
- `automation.lock_front_door_on_goodnight` **KEPT** — uses modern `platform: state` trigger on `scene.goodnight`
- `automation.goodnight_lock_front_door` **DELETED** — used old `event: call_service` trigger, fragile

### Fixed: `automation.plant_1_needs_water_2`
**Root cause:** Automation used a device-based trigger with a UUID entity reference (`f2033445ae28da227c23a910fdf7ead5`) — this type of trigger breaks if the device is reset/re-added, because the UUID changes. The device registry/entity registry APIs confirmed the UUID was non-resolvable via REST.

**Fix applied:** Replaced device trigger with explicit `numeric_state` trigger:
```yaml
trigger: numeric_state
entity_id: sensor.plant_1_soil_moisture
below: 10
for:
  hours: 48
```
Actions unchanged (notify Nathan + Lisa). Automation will now fire reliably when soil moisture drops below 10% for 48 hours. Current moisture: 82.4% — no immediate alert expected.

**Plant automations NOT touched (Nathan's request):**
- `automation.plant_has_enough_water`
- `automation.plant_1_has_enough_water`
- `automation.plant_1_needs_water`
- `automation.plant_1_needs_water_2` (fixed, kept)
- `automation.plant_2_needs_water`

## Backup
Full configs of all affected automations saved to:
`config-backups/automations_2026-04-25_pre-cleanup.yaml`

## Status
- **Before:** 49 automations
- **After:** 44 automations (7 deleted, 1 fixed, 1 kept from merge pair)
- All deletions verified via `/api/states` — none of the 7 entities remain
- Plant automation config verified via `/api/config/automation/config/1737077450232`

## Remaining items from audit (not addressed this session)
- `automation.plant_1_needs_water` — duplicate pair still exists, not deleted per Nathan's request
- `automation.restart_living_room_sensor` — never triggered, trigger config not yet verified
- Plant 2 automations — `automation.plant_2_needs_water` still 460d stale, Plant 2 device offline
