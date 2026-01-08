# Multiplayer Spawn Point System

WORR's multiplayer spawns are built from map entities and then filtered and scored to keep respawns fair and readable. This guide explains what the server looks for, how it falls back when space is tight, and what hosts and map authors can tune.

## Spawn Point Sources

| Entity | Used for | Notes |
| --- | --- | --- |
| `info_player_deathmatch` | FFA and duel spawns | Main pool for non-team modes; also used as fallback in team modes. |
| `info_player_team_red` / `info_player_team_blue` | Team modes | Primary spawns for TDM, CTF, Domination, and other team playlists. |
| `info_player_intermission` | Spectator and intermission camera | Used for spectators and end-of-match views. |
| `info_player_start`, `info_player_coop`, `info_player_coop_lava` | Fallback only | Used only if the map does not provide DM or team spawns. |

## Selection Flow (Deathmatch and Team Modes)

1. Build a candidate list from the map (team list first if the player is active in a team mode).
2. Drop any spot blocked by solid geometry or an occupied player box.
3. Apply soft safety filters when possible:
   - Avoid the last death location (192 units).
   - Skip spawn points with nearby mines or traps (196 units).
   - Keep distance from the nearest living player (160 units).
   - Avoid direct enemy line-of-sight within 2048 units.
4. Score remaining spots with a composite danger score and pick a random winner among the safest ties.

The danger score blends:
- Heat map combat density (50% weight).
- Enemy line-of-sight penalty (20%).
- Nearest-player proximity (15%).
- Last-death proximity (10%).
- Nearby mine or trap penalty (5%).

## Fallbacks and Forced Spawns

- If no eligible spot survives the soft filters, the server relaxes to a lighter fallback set (still avoiding solid geometry and the last death location).
- If the map is temporarily clogged, players are held in a freecam/intermission view while the server retries.
- After a short retry window, a forced spawn ignores player collisions and soft filters but still checks geometry, which can result in a telefrag if space is tight.

## Respawn Timing

- `match_player_respawn_min_delay` gates how soon a player can manually respawn after death.
- `match_force_respawn_time` sets the maximum wait before a respawn is allowed.
- `match_do_force_respawn` controls whether the server auto-respawns at that max time.
- Round-based elimination modes can mark players as eliminated; those players stay in spectator until the round resets.

## Reconnect Ghost Spawns

If the ghost system is active, the server tries to respawn reconnecting players at their saved origin and angles. If the spot is blocked by a player or solid geometry, the ghost spawn is denied and normal spawn selection takes over. Ghost slots only persist after `g_ghost_min_play_time` seconds of match time.

## Spawn Pads (Visual Discs)

Deathmatch spawns can render a pad model to make spawn locations obvious:
- Controlled by `match_allow_spawn_pads` and the map's worldspawn key `no_dm_spawnpads`.
- Suppressed in arena modes, Horde, N64 maps, and non-Quake2 rulesets.
- When pads are enabled, players spawn slightly higher (9 units vs 1) to avoid clipping.

## Map Author Checklist

- Provide enough `info_player_deathmatch` points for FFA/duel and `info_player_team_*` points for team modes.
- Spread spawns to break line-of-sight to major weapons and objectives.
- Avoid tight geometry that can trap the player box or block spawn pads.
- Keep spawn points away from common mine or trap placements.
- Add an `info_player_intermission` so spectators have a clean camera.
- Use `no_dm_spawnpads` in worldspawn if the disc model clashes with your layout.

## Quick Troubleshooting

- Spawning into a freecam briefly usually means no safe spawn was available; the server is retrying.
- Telefrag spawns point to overcrowded or blocked pads; add more spawns or lower player count.
- Missing spawn pads? Check `match_allow_spawn_pads`, `no_dm_spawnpads`, arena or Horde mode, or N64 maps.

For entity details and map keys, see the [Level Designers Guide](level-design.md). For server-side tuning, see the [Cvar Reference](cvars.md).
