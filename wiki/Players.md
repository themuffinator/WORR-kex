# Player Handbook

WORR modernizes Quake II combat with tuned weapon physics, refreshed HUD cues, and a broad gametype roster, plus a practice format for warmups. This handbook summarizes the essentials so you can jump into any lobby prepared.

## Movement & Combat Changes
- **Weapon tuning:** Rockets fly faster and deal consistent damage, Plasma Beam range and knockback are capped, and machinegun families adopt Quake III spread math for predictability.
- **Knockback:** Splash impulses mirror Quake III, enabling reliable rocket jumps and air control adjustments.
- **Ammunition:** Clip sizes and pickups are rebalanced; Bandolier and Ammo Pack respawn faster, so watch timers for resource denial.
- **Health & Tech:** Spawn with +25 temporary health, adrenaline becomes a holdable, and tech regen alternates between health and armor for pacing.
- **Powerups:** Haste, Battle Suit, and Regeneration deliver Quake III-inspired effects, and every powerup can drop on death—protect your carrier.

## UI & Feedback
- WORR’s HUD is adaptive, layering mini-score displays, frag messages, and announcer cues to track match flow without opening the scoreboard.
- Crosshair IDs (`match_crosshair_ids`) are enabled by default so you can confirm team status at a glance.
- Use `kb` and `fm` console commands to customize kill beeps and frag message feeds mid-match.

## Gametype Cheat Sheet
Each gametype exposes distinct objectives and spawn logic. The short codes below appear in the HUD, server browser, and vote menus.

| Code | Name | Core Rules |
| --- | --- | --- |
| `FFA` | Free For All | Classic deathmatch; first to frag limit or highest score at time limit wins. |
| `DUEL` | Duel | 1v1 arena with Marathon queues and no spectators mid-round. |
| `TDM` | Team Deathmatch | Team frags toward shared limit; expect autobalance on public servers. |
| `DOM` | Domination | Capture and hold control points; flips grant bonus points per tick. |
| `CTF` | Capture the Flag | Two-base flag runs with assist/defend scoring. |
| `CA` | Clan Arena | Round-based, no item pickups; loadouts refresh each round. |
| `ONEFLAG/HAR/OVLD` | Objective CTF variants | Neutral flag runs, skull collection, or base core destruction depending on mode. |
| `FT` | Freeze Tag | Freeze enemies, thaw teammates; elimination per round. |
| `STRIKE` | CaptureStrike | Alternating offense/defense rounds with flag plants. |
| `RR` | Red Rover | Eliminated players swap teams; survive the cycle. |
| `LMS/LTS` | Last (Team) Standing | Finite lives; pace your engagements. |
| `HORDE` | Horde Mode | PvE waves with scaling difficulty—coordinate weapon drops. |
| `BALL` | ProBall | Ball carries score by running goals; focus on interceptions. |
| `GAUNTLET` | Gauntlet | Winner stays, loser to the queue; duel fundamentals matter. |

Practice format: set `g_practice 1` to keep the lobby in warmup (no scoring). Disable self-damage with `g_self_damage 0` for drills, or use `gametype none` (`g_gametype 0`) if you want a no-score ruleset outside warmup.

## Voting & Match Etiquette
- Use `callvote` (or shorthand `cv`) to request map, ruleset, or shuffle changes. Available options depend on `g_vote_flags`-check the Call Vote menu before spamming chat.
- Servers often disable mid-match switches via `g_allow_vote_mid_game 0`; wait for intermission before proposing disruptive changes.
- Respect spectator ballots: some hosts allow `g_allow_spec_vote` so observers can fix imbalances without rejoining.

## Tournament Play
- Tournament lobbies lock rosters to social IDs; only listed participants can spawn and the join menu hides join/spectate options.
- Once everyone is ready, the veto menu appears: home picks or bans first, then away, then back to home.
- Captains can still use `tourney_pick`/`tourney_ban` in console, and anyone can check `tourney_status`.
- Ready-up is mandatory for veto and match start.
- Map Choices appears in the join menu after veto, listing the game order.
- If someone disconnects mid-map, the server may trigger a timeout to let them rejoin.

Want the full flow? See the [Tournament Format Guide](Tournaments.md) for config details and veto flow notes.

## Reconnects & Ghosts
WORR’s ghost player system is built to preserve continuity when a player disconnects unexpectedly. It stores a snapshot of your last spawn position and angles, then tries to reuse that space when you return.

### Ghost flow at a glance
- **Ghost capture:** The server caches your last position/angles as a reconnect ghost slot while the auto-ghost system is active.
- **Safety-first checks:** On rejoin, the server validates that the ghost spot is clear of players or map geometry before spawning you there.
- **Fallback protection:** If the spot is blocked, the ghost spawn is denied, the blocker is logged, and normal spawn selection takes over.

### Persistence rules
- **Minimum participation:** Ghost data persists only after you have logged at least `g_ghost_min_play_time` seconds of match time (default `60`). Short joins will not create a ghost slot.
- **State continuity:** When the ghost spawn succeeds, your score, stats, and inventory return with you as part of the ghost system’s persistence.

### Player tips
- **Reconnect fast:** Rejoin quickly after a disconnect so the server can still use your cached spot before the match moves on.
- **Expect a backup spawn:** If you appear elsewhere, your ghost slot was blocked or expired—regroup and keep fighting.
- **Tournament timeouts:** In tournament matches, a disconnect triggers a brief timeout window so you can return to play.

## Quick Console Tips
- `ready`/`notready` toggle your warmup state; countdowns will not start until enough players are marked ready.
- `timeout`/`timein` consume the team’s pause quota; check with teammates before stopping play.
- `mymap <bsp>` queues your preferred map after the current match when the host enables MyMap.

Study the [Cvar Reference](Cvars.md) and [Command Reference](Commands.md) for deeper configuration tweaks that may affect gameplay on specific servers.
