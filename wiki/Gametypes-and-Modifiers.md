# Gametypes and Modifiers Manual

WORR ships 18 competitive gametypes plus a practice format. This manual explains what each mode does, how it scores, and which modifiers change the feel of a match. It is written for players and hosts who need a quick, accurate reference.

## Quick setup
- Switch gametypes with `gametype <short>` or `g_gametype <index>` (see `Commands.md` and `Cvars.md`).
- Keep the lobby in warmup with `g_practice 1` while still using the chosen ruleset.
- Score limits are handled by `fraglimit`, `capturelimit`, `roundlimit`, `timelimit`, and `roundtimelimit`. Mercy rules use `mercylimit`.

## Shared rules and settings
- **Frag-based scoring:** FFA, Duel, TDM, Domination, One Flag, Harvester, Overload, and Head Hunters use `fraglimit` as their points target.
- **Capture or goal scoring:** CTF uses `capturelimit`. ProBall uses `capturelimit` as the goal limit.
- **Round-based flow:** Clan Arena, CaptureStrike, Freeze Tag, Red Rover, Horde, and Gauntlet use `roundlimit` and `roundtimelimit`.
- **Limited lives:** LMS and LTS use `g_lms_num_lives` for starting lives and end when only one player or team has lives remaining.
- **Arena loadouts:** Clan Arena, CaptureStrike, Red Rover, and Gauntlet disable item spawns and use arena starting health and armor (`g_arena_starting_health`, `g_arena_starting_armor`).

## Gametypes
### None (none)
- **Objective:** Sandbox ruleset with no scoring.
- **Scoring:** Disabled; self-damage is off by default.
- **Notes:** Ideal for drills or testing. Use `g_practice 1` if you want warmup with a real ruleset.

### Free For All (ffa)
- **Objective:** Frag anyone, anywhere.
- **Scoring:** `fraglimit` and `timelimit`.
- **Notes:** Classic deathmatch with no teams.

### Duel (duel)
- **Objective:** 1v1 fight to the frag limit.
- **Scoring:** `fraglimit` and `timelimit`.
- **Notes:** `g_allow_duel_queue` controls queueing; `forfeit` can be enabled for concessions.

### Team Deathmatch (tdm)
- **Objective:** Out-frag the other team.
- **Scoring:** `fraglimit` and `timelimit`.
- **Notes:** Friendly fire is set by `g_friendly_fire_scale`; balance with `g_teamplay_force_balance`.

### Domination (dom)
- **Objective:** Capture and hold control points for continuous scoring.
- **Scoring:** Point ticks and capture bonuses; `fraglimit` is the points target.
- **Notes:** Requires Domination control points. See the full [Domination guide](../docs/domination.md).

### Capture The Flag (ctf)
- **Objective:** Steal the enemy flag and return it to your base while your flag is home.
- **Scoring:** `capturelimit` and `timelimit`.
- **Notes:** Supports assists, returns, and standard CTF drop/return rules.

### Clan Arena (ca)
- **Objective:** Eliminate the enemy team each round.
- **Scoring:** `roundlimit` and `roundtimelimit`.
- **Notes:** No item spawns; arena loadouts refresh each round. Round ties break by players remaining, then total health.

### One Flag (oneflag)
- **Objective:** Capture the neutral flag and bring it to your base.
- **Scoring:** `fraglimit` and `timelimit`.
- **Notes:** Uses CTF drop/return behavior; maps need a neutral flag and team obelisks.

### Harvester (har)
- **Objective:** Collect skulls from enemy frags and deliver them to your obelisk.
- **Scoring:** Each skull is worth 1 point; `fraglimit` is the points target.
- **Notes:** Death drops carried skulls; the HUD tracks your skull count.

### Overload (overload)
- **Objective:** Destroy the enemy obelisk to score; defend your own.
- **Scoring:** Points toward `fraglimit`, plus `timelimit` if set.
- **Notes:** Uses CTF-family objectives and obelisk entities.

### Freeze Tag (ft)
- **Objective:** Freeze the entire enemy team.
- **Scoring:** `roundlimit` and `roundtimelimit`.
- **Notes:** On death you freeze instead of respawning. Teammates thaw by staying in range for 3 seconds; pressing Use targets a frozen teammate from farther away. Auto-thaw after `g_frozen_time`.

### CaptureStrike (strike)
- **Objective:** Alternating offense/defense rounds with a flag capture.
- **Scoring:** `roundlimit` and `roundtimelimit`.
- **Notes:** No respawns during the round; wipeouts or captures end it. Only attackers can pick up the flag. If the timer expires, attackers win only if they touched the flag. Arena mode (no item spawns).

### Red Rover (rr)
- **Objective:** Convert the other team.
- **Scoring:** `roundlimit` and `roundtimelimit`.
- **Notes:** Eliminated players respawn on the opposite team; the round ends when one team has no players. Arena mode (no item spawns).

### Last Man Standing (lms)
- **Objective:** Survive with limited lives.
- **Scoring:** Last player with lives wins; `g_lms_num_lives` sets starting lives.
- **Notes:** `timelimit` still applies if set.

### Last Team Standing (lts)
- **Objective:** Team version of LMS.
- **Scoring:** Last team with lives wins; `g_lms_num_lives` sets starting lives.
- **Notes:** Protect teammates to preserve the shared life pool.

### Horde (horde)
- **Objective:** Co-op survival against monster waves.
- **Scoring:** `roundlimit` for total waves and `roundtimelimit` per wave if set.
- **Notes:** Waves spawn from deathmatch spawn points; `g_horde_starting_wave` sets the entry wave.

### Head Hunters (hh)
- **Objective:** Collect heads and bank them at receptacles.
- **Scoring:** Triangular scoring per deposit; `fraglimit` is the points target; carry limit 20.
- **Notes:** Requires `headhunters_receptacle` entities. See the full [Head Hunters guide](../docs/headhunters.md).

### ProBall (ball)
- **Objective:** Carry or pass the ball into the enemy goal.
- **Scoring:** `capturelimit` sets the goal limit; `timelimit` applies.
- **Notes:** Only the ball spawns. Goals and out-of-bounds reset the ball to spawn; assists within 8 seconds award a point to the assister. Maps need `item_ball`, `trigger_proball_goal`, and `trigger_proball_oob`.

### Gauntlet (gauntlet)
- **Objective:** Rotating 1v1 ladder; winner stays, loser goes to the back of the queue.
- **Scoring:** `roundlimit` and `roundtimelimit`.
- **Notes:** Arena mode (no item spawns). `g_allow_duel_queue` controls queueing, and `forfeit` is available when enabled.

## Modifiers
### Standard
- **Effect:** No special modifiers are active.

### InstaGib
- **Effect:** Railgun-only loadout with one-shot rail hits and infinite slugs.
- **Settings:** `g_instaGib 1` (latched). Optional splash via `g_instagib_splash 1`.
- **Notes:** Item spawns are disabled while InstaGib is active.

### Vampiric Damage
- **Effect:** Deal damage to heal yourself.
- **Settings:** `g_vampiric_damage 1`, `g_vampiric_percentile`, `g_vampiric_health_max`.
- **Notes:** Overheal decays above `g_vampiric_exp_min`; health pickups are disabled.

### Weapons Frenzy
- **Effect:** Faster fire, faster rockets, and ammo regeneration.
- **Settings:** `g_frenzy 1` (latched).
- **Notes:** Weapon switching is effectively instant while Frenzy is active.

### Gravity Lotto
- **Effect:** Gravity shifts to a random value between 100 and 2000 every 2 minutes.
- **Settings:** `g_gravity_lotto 1` (live); uses `g_gravity` to set the active value.
- **Notes:** Announced to all players mid-match.

### Additional server toggles
- **Quad Hog:** `g_quadhog 1` limits Quad Damage to a single holder at a time (latched).
- **Nade Fest:** `g_nadeFest 1` forces grenade-focused loadouts (latched).
- **Notes:** The setup menu expects only one modifier. If multiple are enabled, the UI announces the first active modifier it detects.
