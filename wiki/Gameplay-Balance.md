# Gameplay Balance

This page consolidates the live gameplay balance in WORR-KEX and compares key values with the original Quake II rerelease codebase. It draws on the design outline in `docs/gameplay.html` and cross-references the current implementation to highlight where WORR diverges from id Software's defaults.

## Weapon tuning

### Rocket Launcher
- WORR fixes rocket damage at 100 with a 100-unit splash radius and increases projectile speed to 800 UPS by default (1000 in Quake 1 rulesets and 900 under Quake 3 rules). In Quake II the rocket dealt 100–120 variable damage, used a 120-unit splash radius, and travelled at 650 UPS.

### Plasma Beam
- In deathmatch the plasma beam now inflicts 8 damage with 8 points of knockback, while single-player keeps the 15-damage baseline (30 in Quake 1 rulesets). Knockback scales with the chosen damage value. The beam length is capped at 768 units (600 in Quake 1 rulesets). Originally the Rogue “heatbeam” dealt 15 damage in deathmatch with 75 points of knockback and effectively unlimited range until a collision.

### Hunter & Vengeance spheres
- Hunter, Vengeance, and Defender spheres now expire after 10 seconds instead of 30.
- The hunter sphere’s chase speed is reduced to 300 UPS (down from 500), although it still surges to 1000 UPS during its final attack dash. This curbs pursuit strength while keeping the high-speed finishing burst.

### Hitscan spread (machinegun, chaingun, shotgun)
- WORR raises the default bullet spread cone to 500 units horizontally and vertically, replacing Quake II’s 300×500 box spread. Shotgun constants remain 1000×500, matching the legacy values.
- The machinegun continues to fire eight-damage shots but now uses the wider spread, with Quake 3 rulesets reducing damage and narrowing spread to 200×200 for tighter duels.

### Haste fire-rate scaling
- Weapon animation timing multiplies the base gun rate by 1.5 whenever Haste is active, delivering the advertised 50 % fire-rate boost.

## Item economy

### Ammo capacities and pickups

| Ammo | WORR max (base / bandolier / pack) | Quake II max (base / bandolier / pack) | Pickup amounts (ammo / weapon / bandolier / pack) |
| --- | --- | --- | --- |
| Bullets | 200 / 250 / 300 | 200 / 250 / 300 | 50 / 50 / 50 / 30 |
| Shells | 50 / 100 / 150 | 100 / 150 / 200 | 10 / 10 / 20 / 10 |
| Rockets | 25 / 25 / 50 | 50 / 50 / 100 | 10 / 5 / 0 / 5 |
| Grenades | 25 / 25 / 50 | 50 / 50 / 100 | 10 / 5 / 0 / 5 |
| Cells | 200 / 200 / 300 | 200 / 250 / 300 | 50 / 50 / 0 / 30 |
| Slugs | 25 / 25 / 50 | 50 / 75 / 100 | 10 / 5 / 0 / 5 |

WORR therefore cuts rocket, grenade, and slug stockpiles roughly in half while leaving pickup quantities unchanged, tightening explosive and precision ammo management.

Bandoliers and ammo packs still grant the bonus ammo listed above but now respawn faster (30 s for the bandolier, 90 s for the ammo pack). Bandolier and pack pickups continue to adjust the player’s maximum ammo through the shared `ammoStats` table.

### Spawn health and regeneration
- Deathmatch spawns grant a configurable health bonus (25 by default, or the Quake 3 value under RS_Q3A). The bonus is tracked in `healthBonus` and decays at one point per second until the player returns to their nominal maximum.
- Mega Health pickups run a timer that persists across multiple grabs; the item ticks health back toward the stored threshold before respawning.
- Adrenaline is a reusable holdable in deathmatch, granting +5 to max health (and +1 elsewhere).

### Power armor
- WORR equalizes power armor absorption: both power screen and shield consume one cell per point of prevented damage in deathmatch. In Quake II, the shield spent two cells per point, making it substantially weaker.

### Powerups
- All major powerups remain droppable on death when the server enables powerup drops.
- Picking up a powerup in deathmatch schedules a 120-second respawn unless it was a dropped item; initial map spawns hide powerups for a random 30–60 seconds to stagger control routes.
- Using Haste, Battle Suit, Double Damage, Regeneration, or related powerups consumes the item and grants 30 seconds of effect by default (or the remaining drop timeout). Combined with the 1.5× gun-rate multiplier above, Haste materially accelerates combat pacing.

## Player spawning and the combat heatmap

- Every time damage is applied the combat heatmap records a weighted event and decays over time. `HM_AddEvent` maps each hit into 256-unit cells with a cosine falloff, while `HM_Query` and `HM_DangerAt` aggregate danger scores in a configurable radius.
- The system initializes when the game starts and resets whenever a new map loads.
- Spawn selection blends the heatmap with several live factors. `CompositeDangerScore` weights recent combat (50 %), enemy line-of-sight (20 %), proximity to other players (15 %), the player’s death spot (10 %), and nearby mines (5 %) to score each spawn. `SelectDeathmatchSpawnPoint` shuffles initial lists, filters unusable spots, falls back to team and classic spawn points when needed, and finally picks the lowest-danger candidate within a tolerance band. This process delivers the heatmap-driven spawn behaviour described in the gameplay brief.

