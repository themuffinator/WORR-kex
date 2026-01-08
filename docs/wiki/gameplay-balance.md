# Gameplay Balance Changes

WORR-KEX tunes Quake II combat for faster, more readable fights. This page lists the live balance changes for the default multiplayer ruleset (Quake II). Quake 1 and Quake 3 rulesets override a few numbers; callouts below note those exceptions.

## Weapons

### Rocket Launcher
- Damage is fixed at 100 (no random roll) with a 100-unit splash radius.
- Projectile speed is 800 UPS (900 in Quake 3 ruleset, 1000 in Quake 1 ruleset).

### Plasma Beam
- Max range is capped at 768 units (600 in Quake 1 ruleset).
- Multiplayer damage and knockback are 8 per tick (single-player keeps 15; Quake 1 ruleset uses 30).

### Hunter and Vengeance Spheres
- Lifespans are 10 seconds instead of 30.
- Hunter chase speed is 300 UPS (down from 500), but the final attack dash still spikes to 1000 UPS.

### Hitscan Spread
- Machinegun and chaingun use a Quake III style sin-cone spread at 500x500.
- Shotgun and super shotgun use the Quake III cone projection with 1000x500 spread.

### Knockback and Splash Physics
- Radial damage follows Quake III style knockback math for more predictable rocket and grenade jumps.

## Ammo Economy

| Ammo | Max (base / bandolier / pack) | Pickup amounts (ammo / weapon / bandolier / pack) |
| --- | --- | --- |
| Bullets | 200 / 250 / 300 | 50 / 50 / 50 / 30 |
| Shells | 50 / 100 / 150 | 10 / 10 / 20 / 10 |
| Rockets | 25 / 25 / 50 | 10 / 5 / 0 / 5 |
| Grenades | 25 / 25 / 50 | 10 / 5 / 0 / 5 |
| Cells | 200 / 200 / 300 | 50 / 50 / 0 / 30 |
| Slugs | 25 / 25 / 50 | 10 / 5 / 0 / 5 |
| Mag Slugs | 25 / 25 / 50 | 10 / 5 / 0 / 5 |
| Flechettes | 100 / 150 / 200 | 50 / 50 / 50 / 30 |
| Prox Mines | 10 / 10 / 20 | 5 / 5 / 0 / 5 |
| Rounds | 6 / 6 / 12 | 3 / 3 / 0 / 3 |
| Traps | 3 / 3 / 12 | 1 / 1 / 0 / 0 |
| Tesla Mines | 3 / 3 / 12 | 1 / 1 / 0 / 0 |

Bandoliers respawn every 30 seconds and Ammo Packs every 90 seconds, keeping resource routes active.

## Health and Armor

- Spawn health is `g_starting_health` (default 100) plus `g_starting_health_bonus` (default +25) that decays 1 per second back to base.
- Mega Health decay persists across consecutive pickups, so stacking extends the buffer instead of restarting it.
- Stimpacks heal 3.
- Adrenaline is a holdable in multiplayer (outside duel presets) and increases max health by 5.
- Power Armor in multiplayer uses 1 cell per absorbed damage for both screen and shield types; energy hits still drain extra cells.

## Powerups

- Powerups spawn 30 to 60 seconds after map start in deathmatch, then respawn every 120 seconds.
- Activations last 30 seconds by default; dropped powerups keep their remaining time.
- Haste replaces the old Quadfire style powerup: +50 percent fire rate and +50 percent movement speed.
- Battle Suit replaces Invulnerability: blocks splash damage and halves remaining direct or environmental damage.
- Regeneration (from Quake III) restores health over time up to your max.
- Invisibility is stronger than stock for clearer stealth play.
- Powerups drop on death when `match_powerup_drops` is enabled (default on) and announce spawns and pickups globally.

## Techs

- AutoDoc ticks once per second, restoring 5 health up to 150 and then 5 armor once health is capped.
- Tech ownership and drops follow the classic one-tech-at-a-time flow, but the faster tick makes timing choices matter more.

## Spawn Safety

- Deathmatch spawns avoid recent combat hotspots and nearby threats using a heatmap, reducing mid-fight spawn kills.

## Related Settings

Server hosts can fine-tune most of these values. See the [Cvar Reference](cvars.md) and the [Server Hosts Guide](server-hosts.md) for the relevant knobs.
