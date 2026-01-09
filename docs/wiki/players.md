# Player Guide

## Movement and Combat Updates
- **Rocket Launcher:** Faster rockets (800 UPS vs. 650) with fixed 100 damage tighten timing for splash plays and air denial.
- **Plasma Beam:** The beam now stops at 768 units, deals 8 damage per tick (down from 15), and barely pushes targets (knockback 8). Expect closer duels and less juggling.
- **Hunter & Vengeance Spheres:** Slower travel (300 UPS) and shorter 10-second lifespan reduce map-wide pressure; plan ambushes carefully.
- **Bullet Weapons:** Machinegun and Chaingun scatter more vertically, and the shotgun family now mirrors Quake III’s cone spread—burst fire to stay accurate.
- **Knockback Model:** Radial damage now follows Quake III physics, making rocket and grenade jumps feel predictable; rehearse angles knowing the launch math stays consistent.
- **Ammo Economy:** Expect larger reserves on bullets, flechettes, and cells plus halved respawn times for Bandoliers (30s) and Ammo Packs (90s). Aggressive players can keep pressure with mindful pickup routes.
- **Health Flow:** +25 bonus spawn health decays to 100, Mega Health timers stack, and Stimpacks heal 3. Adrenaline is holdable outside duels and adds +5 max health—stash it before big pushes.
- **Power Armor & Powerups:** Power Armor always soaks 1 damage per cell. Haste grants +50% rate of fire and speed, Battle Suit halves direct hits and blocks splash, Regeneration heals over time, and all major powerups announce spawns/pickups globally to fuel fights.

## UI and Feedback
- **Adaptive HUD:** The default overlay surfaces only the essentials you need mid-fight while adapting to context so situational awareness stays high.
- **Score Awareness:** Mini-score displays and frag messages sit in the HUD, keeping streaks and team status visible without chat scrolling.
- **Match Announcer:** Key events—from powerup grabs to lead changes—play through a dynamic announcer layer, reinforcing callouts for players without voice comms.

## Gametype Cheat Sheet
| Mode | Console Short Name | Core Focus & Notes | Quick Reference |
| --- | --- | --- | --- |
| Free For All | `ffa` | Classic deathmatch; highest frag count wins. | - |
| Duel | `duel` | 1v1 spotlight with frag scoring; ideal for focused skill checks. | - |
| Team Deathmatch | `tdm` | Teams race to frag limit; communication decides trades. | - |
| Domination | `dom` | Capture and hold control points for continuous scoring; flip bonuses reward aggression. | [Domination guide](../domination.md) |
| Capture The Flag | `ctf` | Flag runs and returns define the pace. | - |
| Clan Arena | `ca` | Round-based team elimination with arena loadouts. | - |
| One Flag | `oneflag` | Shared neutral flag-coordinate escorts both ways. | - |
| Harvester | `har` | Collect enemy skulls and score at your base. | - |
| Head Hunters | `hh` | Collect dropped heads and cash them in at receptacles for scoring bursts. | [Head Hunters guide](../headhunters.md) |
| Overload | `overload` | Destroy the enemy obelisk to score; defend your own. | - |
| Freeze Tag | `ft` | Freeze foes instead of fragging; thaw teammates to win rounds. | - |
| CaptureStrike | `strike` | Hybrid round play with capture objectives and elimination stakes. | - |
| Red Rover | `rr` | Swapping sides on death keeps pressure constant; manage spawns. | - |
| Last Man Standing | `lms` | Everyone gets limited lives-play cautiously. | - |
| Last Team Standing | `lts` | Team variant of LMS; protect allies' life pools. | - |
| Horde Mode | `horde` | Survive PvE waves with periodic breaks. | - |
| ProBall | `ball` | Team sports twist-control the ball to score. | - |
| Gauntlet | `gauntlet` | Duel-centric rounds emphasizing precision frags. | - |

## Practice Format
- Set `g_practice 1` to keep the lobby in warmup (no scoring) while still using your chosen gametype.
- Disable self-damage for drills with `g_self_damage 0` if the host allows it.
- Use `gametype none` (`g_gametype 0`) only when you want a no-score, no self-damage ruleset outside the warmup flow.

> **Tip:** Loadouts, scoring rules, and round flow come from the flags defined in `GAME_MODES`. The console short name is the value to feed `g_gametype` or the Call Vote menu. For warmups, keep `g_practice 1` so the lobby stays in warmup. Consult mode-specific docs (e.g., Domination above) when a lobby needs deeper strategy, and map authors can reference the [Entity Catalogue](level-design.md#entity-catalogue) to double-check spawn and objective coverage before sharing workshop builds.

## Voting and Match Etiquette
- Want the complete syntax for `callvote`, ready commands, or spectator tools? Check the [Command Reference](commands.md) for detailed usage notes to share with teammates before calling for action.
- **How votes unlock:** Server hosts mask vote commands with `g_vote_flags`. Each bit toggles an item (map, restart, gametype, limits, shuffle/balance, unlagged, arena, forfeit, etc.). Default servers enable all flags (`16383`), showing every option.
- **Reading the menu:** If a choice is missing, the host likely cleared that bit-ask before spamming chat, and remember hosts may restrict disruptive calls like `shuffle` during events.
- **Etiquette:** Call votes with a clear reason ("Restart for overtime bugged scoreboard") and allow the countdown to finish. Avoid chaining failed votes; wait a few minutes or until the match state changes. Hosts appreciate players rallying support in team chat before triggering global prompts.
- **Want to know the knobs?** The [Cvar Reference](cvars.md#voting-admin-and-moderation) breaks down which server toggles influence the vote menu, warmup readiness, and timeout privileges.

## Tournament Play
- Tournament lobbies lock rosters to social IDs; only listed participants can spawn and the join menu hides join/spectate options.
- Once everyone is ready, the veto menu appears: home picks or bans first, then away, then back to home.
- Captains can still use `tourney_pick`/`tourney_ban` in console, and anyone can check `tourney_status`.
- Ready-up is mandatory for veto and match start.
- Map Choices appears in the join menu after veto, listing the game order.
- If someone disconnects mid-map, the server may trigger a timeout to let them rejoin.

Want the full flow? See the [Tournament Format Guide](tournaments.md) for config details and veto flow notes.

## Ghost Player System (Reconnect Safeguards)
WORR’s ghost player system is a continuity safety net for unexpected disconnects. It records a snapshot of your last valid spawn location and angles, then tries to honor that spot if you return quickly.

### How it works
- **Ghost capture:** When the auto-ghost system is active, the server caches your last position/angles as a reconnect ghost slot.
- **Safety-first respawn:** On rejoin, the server checks the saved spot for blocking players or geometry before placing you there.
- **Fallback logic:** If anything is obstructing the ghost spot, the server logs the blocker and falls back to normal spawn selection so you are never trapped.

### Persistence rules
- **Minimum participation:** Ghost data is only saved after you have logged at least `g_ghost_min_play_time` seconds of real match time (default `60`). Leave earlier and the slot clears, preventing accidental ghost saves from brief joins.
- **State continuity:** When the ghost spawn succeeds, your score, stats, and inventory return with you as part of the ghost system’s persistence.

### Player tips
- **Reconnect fast:** Rejoin promptly after a disconnect so the server can still use your cached spot before the match state moves on.
- **Don’t panic on a new spawn:** If you appear elsewhere, it means your ghost slot was blocked or expired; regroup and continue without losing momentum.
- **Tournament timeouts:** In tournament matches, a disconnect triggers a brief timeout window so you can return to play.
