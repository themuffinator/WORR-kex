# WORR Console Command Reference

Commands are grouped by responsibility so hosts, admins, and players can locate the verbs they need quickly. Access restrictions derive from the registration flags in the command modules—commands marked with `AdminOnly` require successful `/admin <password>` login, while `CheatProtect` follows the `cheats` cvar.

## Player & Spectator Commands
| Command | Access | Summary |
| --- | --- | --- |
| `admin` | Spectators & intermission | Opens the admin login prompt when you know the `admin_password`. |
| `clientlist` | All players | Prints connection slots and ping/state info for troubleshooting. |
| `drop` / `dropindex` | Live players | Drop current weapon or a specific inventory index. |
| `eyecam` | Spectators | Toggles chase camera to orbit points of interest. |
| `follow`, `followkiller`, `followleader`, `followpowerup` | Dead players & spectators | Cycle chase targets during spectating. |
| `forfeit` | Live players | Requests a team forfeit in elimination modes (subject to server policy). |
| `help` / `inven` / `score` | All | Display usage help, inventory browser, or scoreboard without leaving the arena. |
| `hook` / `unhook` | All | Engage or release the grappling hook when enabled. |
| `id` | All | Toggles crosshair IDs when `match_crosshair_ids` is active. |
| `invnext*` / `invprev*` / `invuse` | All | Cycle through and use inventory slots (weapons, powerups). |
| `kb` | All | Toggle kill beep feedback locally. |
| `kill` | Live players | Suicide command (respecting `g_allow_kill`). |
| `mapcycle` / `mappool` / `mapinfo` | All | Inspect rotation contents and per-map metadata pulled from the JSON pool. |
| `motd` | Spectators & intermission | Re-read the server MOTD file. |
| `mymap` | All | Queue a MyMap pick when hosts enable the feature. |
| `ready` / `readyup` / `ready_up` / `notready` | All | Control warmup ready state to start matches. |
| `setweaponpref` | All | Persist preferred weapon ordering for spawns. |
| `sr` | All | Display personal skill rating estimate used for balance. |
| `stats` | Spectators & intermission | Show detailed match stats overlay. |
| `team` | Dead players & spectators | Join or switch teams when allowed. |
| `timeout` / `timein` / `timer` | All | Consume timeouts, resume play, or show personal timers. |
| `use*` | All | Activate items by name or index (weapons, techs). |
| `weapnext` / `weapprev` / `weaplast` | All | Cycle weapon inventory in either direction. |
| `where` | Spectators | Print current coordinates for callouts or mapping. |

## Map Voting & Governance
| Command | Access | Summary |
| --- | --- | --- |
| `callvote <topic>` / `cv` | Dead players & spectators | Start a vote for map, mode, shuffle, or ruleset as allowed by `g_vote_flags`. Syntax is topic-specific (e.g., `callvote map q2dm1`). |
| `vote <yes|no>` | Dead players | Cast a ballot on the active vote prompt. |

## Administrative Commands
These require a logged-in admin user (see `/admin`).

| Command | Purpose |
| --- | --- |
| `add_admin` / `remove_admin` | Manage the admin roster file on disk. |
| `add_ban` / `remove_ban` / `load_bans` | Maintain IP ban lists without restarting. |
| `arena` | Force a specific arena layout in Arena/RA2 playlists. |
| `balance` / `shuffle` | Trigger skill-based team balancing or random shuffles. |
| `boot` | Kick a player from the server (with messaging). |
| `end_match` / `reset_match` / `start_match` | Control match lifecycle manually (end now, wipe scores, start immediately). |
| `force_vote` | Override the current vote result (force pass/fail). |
| `gametype` / `ruleset` | Switch active gametype or ruleset instantly (`gametype practice` enables no-score warmups without self-damage). |
| `load_mappool` / `load_mapcycle` / `load_motd` | Reload map or MOTD assets from disk after edits. |
| `lock_team` / `unlock_team` | Prevent or allow team joins for specific colors. |
| `map_restart` / `next_map` / `set_map` | Restart the current map, advance to cycle entry, or load a specific BSP. |
| `ready_all` / `unready_all` | Force lobby participants into (or out of) ready state. |
| `set_team` | Move a named player to a team slot manually. |

## Cheat & Development Utilities
These commands are guarded by the `cheats` cvar and primarily support offline testing.

| Command | Summary |
| --- | --- |
| `give`, `god`, `immortal`, `noclip`, `notarget`, `teleport` | Standard Quake-style cheat toggles for inventory, invulnerability, movement, and relocation. |
| `alert_all` | Broadcast a center-print message to all players for announcements. |
| `check_poi` / `set_poi` / `target` | Inspect and manipulate saved points-of-interest for scripted sequences. |
| `clear_ai_enemy` / `kill_ai` | Reset or slay targeted AI actors while debugging encounters. |
| `list_entities` / `list_monsters` | Dump active entity or monster tables to the console with optional filtering. |
| `novisible` | Toggle visibility checks for testing stealth and fog volumes. |

## Tips for Hosts
- Combine admin commands with matching cvar changes (e.g., `set g_vote_flags 1535`) to ensure your policy updates take effect immediately.
- Document any non-default command flows (like forcing `/forfeit` in tournaments) in match rules so players understand expectations.
- Pair this reference with the [Cvar Guide](Cvars.md) when adjusting rules mid-event to avoid conflicting settings.
