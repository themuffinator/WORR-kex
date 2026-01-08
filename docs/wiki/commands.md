# WORR Command Reference

This guide consolidates the console commands exported by WORR's server module, grouped by the jobs they solve for hosts, admins, and players. Each entry calls out syntax, permission requirements, and a practical console example.

## Permission flags at a glance

Commands expose access rules through `CommandFlag` bitmasks:

- **`AllowDead`** – usable while dead or in limbo.
- **`AllowIntermission`** – callable during the post-match screen.
- **`AllowSpectator`** – callable from spectator slots.
- **`MatchOnly`** – restricted to live match states.
- **`AdminOnly`** – requires an authenticated admin session.
- **`CheatProtect`** – requires cheats enabled (single-player or developer servers).

These flags appear in each `RegisterCommand` call alongside the handler function. Flood-exempt commands are marked in the source with a trailing `true` argument.

---

## Admin & host workflows

### Moderation and policy

- **`add_admin`** — Adds a player's social ID to `admin.txt`, reloads the list, and announces the promotion.  
  - *Syntax:* `add_admin <client#|name|social_id>`  
  - *Permissions:* Admin-only; allowed while spectating or during intermission.  
  - *Example:* `\add_admin EOS:ABCDEF0123456789ABCDEF0123456789`
- **`remove_admin`** — Removes a social ID from `admin.txt` (except the lobby host) and refreshes the roster.  
  - *Syntax:* `remove_admin <client#|name|social_id>`  
  - *Permissions:* Admin-only; usable while spectating or during intermission.  
  - *Example:* `\remove_admin EOS:...`
- **`add_ban`** — Resolves the target to a social ID, blocks banning listed admins or the host, and appends the ID to `ban.txt`.  
  - *Syntax:* `add_ban <client#|name|social_id>`  
  - *Permissions:* Admin-only; usable while spectating or during intermission.  
  - *Example:* `\add_ban NX:12345678901234567`
- **`remove_ban`** — Removes a social ID from `ban.txt` and reloads the ban cache.  
  - *Syntax:* `remove_ban <social_id>`  
  - *Permissions:* Admin-only; usable while spectating or during intermission.  
  - *Example:* `\remove_ban Steamworks:7656119...`
- **`load_admins`** / **`load_bans`** — Reload the cached admin or ban list after manual file edits.  
  - *Syntax:* `load_admins` or `load_bans`  
  - *Permissions:* Admin-only; usable while spectating or during intermission.  
  - *Example:* `\load_admins`
- **`boot`** — Kicks a player unless they are the lobby host or an admin, using the engine's `kick` command behind the scenes.  
  - *Syntax:* `boot <client name|number>`  
  - *Permissions:* Admin-only; usable while spectating or during intermission.  
  - *Example:* `\boot troublemaker`

### Match control and rosters

- **`start_match`** — Forces the match out of warmup into live play when it has not already started.  
  - *Syntax:* `start_match`  
  - *Permissions:* Admin-only; usable while spectating or during intermission.  
  - *Example:* `\start_match`
- **`end_match`** — Triggers intermission immediately if a match is in progress and not already finished.  
  - *Syntax:* `end_match`  
  - *Permissions:* Admin-only; usable while spectating or during intermission.  
  - *Example:* `\end_match`
- **`reset_match`** - Restarts the live match after confirming it has begun and is not already at intermission.  
  - *Syntax:* `reset_match`  
  - *Permissions:* Admin-only; usable while spectating or during intermission.  
  - *Example:* `\reset_match`
- **`replay`** - Replays a specific tournament game in the current match set (confirmation required).  
  - *Syntax:* `replay <game#> [confirm]`  
  - *Permissions:* Admin-only; usable while spectating or during intermission.  
  - *Example:* `\replay 2 confirm`
- **`map_restart`** — Issues a `gamemap` reload for the current BSP, effectively soft-restarting the server session.  
  - *Syntax:* `map_restart`  
  - *Permissions:* Admin-only; usable while spectating or during intermission.  
  - *Example:* `\map_restart`
- **`ready_all`** / **`unready_all`** — Force every player into or out of ready state after validating warmup requirements.  
  - *Syntax:* `ready_all` / `unready_all`  
  - *Permissions:* Admin-only; usable while spectating or during intermission.  
  - *Example:* `\ready_all`
- **`force_vote`** — Resolves the current vote to yes or no, applying the action or cancelling it immediately.  
  - *Syntax:* `force_vote <yes|no>`  
  - *Permissions:* Admin-only; usable while spectating or during intermission.  
  - *Example:* `\force_vote yes`
- **`balance`** — Calls the team balancer to redistribute players by score/skill.  
  - *Syntax:* `balance`  
  - *Permissions:* Admin-only; usable while spectating or during intermission.  
  - *Example:* `\balance`
- **`shuffle`** — Shuffles teams using the skill-based algorithm.  
  - *Syntax:* `shuffle`  
  - *Permissions:* Admin-only; usable while spectating or during intermission.  
  - *Example:* `\shuffle`
- **`set_team`** — Moves a specific client to a named team, validating gametype restrictions and skipping redundant moves.  
  - *Syntax:* `set_team <client> <red|blue|spectator|free>`  
  - *Permissions:* Admin-only; usable while spectating or during intermission.  
  - *Example:* `\set_team 7 blue`
- **`lock_team`** / **`unlock_team`** — Toggle whether Red or Blue can accept joins, with feedback if the requested state already matches.  
  - *Syntax:* `lock_team <red|blue>` / `unlock_team <red|blue>`  
  - *Permissions:* Admin-only; usable while spectating or during intermission.  
  - *Example:* `\lock_team red`

### Map, rules, and arena tools

- **`set_map`** — Validates the requested map against the pool, announces the change, and queues a level transition.  
  - *Syntax:* `set_map <mapname>`  
  - *Permissions:* Admin-only; usable while spectating or during intermission.  
  - *Example:* `\set_map q2dm1`
- **`next_map`** — Ends the match to advance into the rotation-defined next map.  
  - *Syntax:* `next_map`  
  - *Permissions:* Admin-only; usable while spectating or during intermission.  
  - *Example:* `\next_map`
- **`arena`** — Reports the current arena when called without arguments or forces a new arena after validation in multi-arena modes.  
  - *Syntax:* `arena [number]`  
  - *Permissions:* Admin-only; callable while spectating (intermission restricted).  
  - *Example:* `\arena 3`
- **`gametype`** - Lists available gametypes on `?` and switches modes when supplied a valid identifier; `none` sets a no-score ruleset (also disables self-damage). For persistent warmup sessions, set `g_practice 1`.  
  - *Syntax:* `gametype <name>`  
  - *Permissions:* Admin-only; usable while spectating or during intermission.  
  - *Example:* `\gametype duel`
- **`ruleset`** — Shows the active ruleset and applies a new one by identifier, updating the `g_ruleset` cvar.  
  - *Syntax:* `ruleset <q1|q2|q3a>`  
  - *Permissions:* Admin-only; usable while spectating or during intermission.  
  - *Example:* `\ruleset q3a`
- **`load_mappool`** / **`load_mapcycle`** — Reload map pool and rotation definitions from disk, optionally chaining both reloads for the pool command.  
  - *Syntax:* `load_mappool` / `load_mapcycle`  
  - *Permissions:* Admin-only; usable while spectating or during intermission.  
  - *Example:* `\load_mappool`
- **`load_motd`** — Reloads the Message of the Day text into memory.  
  - *Syntax:* `load_motd`  
  - *Permissions:* Admin-only; usable while spectating or during intermission.  
  - *Example:* `\load_motd`

---

## Player & spectator utilities

### Access, readiness, and team flow

- **`admin`** — Displays admin status or consumes the configured password to grant admin rights when allowed.  
  - *Syntax:* `admin [password]`  
  - *Permissions:* Available to all players and spectators, including during intermission.  
  - *Example:* `\admin mySecret`
- **`team`** — Shows current team when used without arguments or switches to the requested team (spectator/free validated).  
  - *Syntax:* `team [red|blue|spectator|free]`  
  - *Permissions:* Usable while dead or spectating.  
  - *Example:* `\team red`
- **`ready`**, **`ready_up`/`readyup`**, **`notready`** — Toggles a player's ready state or toggles the “ready up” countdown flag after verifying warmup conditions.  
  - *Syntax:* `ready` | `ready_up` | `readyup` | `notready`  
  - *Permissions:* Usable while dead; flood-exempt for quick warmup coordination.  
  - *Example:* `\ready`
- **`forfeit`** — Allows the losing Duel/Gauntlet player to concede mid-match when forfeits are enabled.  
  - *Syntax:* `forfeit`  
  - *Permissions:* Usable while dead; flood-exempt.  
  - *Example:* `\forfeit`
- **`timeout`** / **`timein`** - Starts a timeout (respecting per-player limits) or ends one if called by the owner or an admin.  
  - *Syntax:* `timeout` / `timein`  
  - *Permissions:* Usable while dead or spectating.  
  - *Example:* `\timeout`
- **`timer`** - Toggles the HUD match timer widget for the caller.  
  - *Syntax:* `timer`  
  - *Permissions:* Usable while dead or spectating.  
  - *Example:* `\timer`
- **`putaway`** - Closes active menus, scoreboards, and help screens, restoring the regular HUD.  
  - *Syntax:* `putaway`  
  - *Permissions:* Usable while spectating.  
  - *Example:* `\putaway`

### Tournament veto tools

- Tournament vetoes are menu-driven; captains (or the home/away players in FFA) can still use the commands below when needed.
- **`tourney_pick`** - Selects a map for the tournament series during the veto phase (captain only).  
  - *Syntax:* `tourney_pick <mapname>`  
  - *Permissions:* Usable while dead or spectating.  
  - *Example:* `\tourney_pick q2dm1`
- **`tourney_ban`** - Bans a map from the tournament series during the veto phase (captain only).  
  - *Syntax:* `tourney_ban <mapname>`  
  - *Permissions:* Usable while dead or spectating.  
  - *Example:* `\tourney_ban q2dm2`
- **`tourney_status`** - Prints the current tournament pool, picks, bans, and whose turn is next.  
  - *Syntax:* `tourney_status`  
  - *Permissions:* Usable while dead or spectating.  
  - *Example:* `\tourney_status`

### Spectating and camera tools

- **`follow`** — As a spectator, lock the camera onto a named or numbered player after validating they are active.  
  - *Syntax:* `follow <client name|number>`  
  - *Permissions:* Usable by spectators or dead players; flood-exempt for menu bindings.  
  - *Example:* `\follow 3`
- **`followkiller`**, **`followleader`**, **`followpowerup`** — Toggle auto-follow helpers that snap to your killer, top fragger, or current powerup carrier.  
  - *Syntax:* `followkiller` | `followleader` | `followpowerup`  
  - *Permissions:* Usable by spectators or dead players; flood-exempt.  
  - *Example:* `\followpowerup`
- **`eyecam`** — Toggles EyeCam first-person spectating mode.  
  - *Syntax:* `eyecam`  
  - *Permissions:* Spectator-only.  
  - *Example:* `\eyecam`
- **`id`** — Toggles crosshair nameplates on hovered players.  
  - *Syntax:* `id`  
  - *Permissions:* Usable while dead or spectating.  
  - *Example:* `\id`
- **`where`** — Prints and copies your current coordinates and view angles for callouts or bug reports.  
  - *Syntax:* `where`  
  - *Permissions:* Spectator-only.  
  - *Example:* `\where`

### Inventory, weapons, and mobility

- **`drop`** / **`dropindex`** — Drops an item by name, special keyword (`tech`/`weapon`), or inventory index, respecting server drop restrictions and notifying teammates when enabled.  
  - *Syntax:* `drop <item|tech|weapon>` or `dropindex <index>`  
  - *Permissions:* Available to active players (no special flags).  
  - *Example:* `\drop quad`
- **`invdrop`** — Drops the currently selected inventory item if it supports dropping.  
  - *Syntax:* `invdrop`  
  - *Permissions:* Available to active players.  
  - *Example:* `\invdrop`
- **`inven`** — Toggles the join/inventory menu in multiplayer or the inventory display in other modes.  
  - *Syntax:* `inven`  
  - *Permissions:* Usable while dead or spectating; flood-exempt for menu binding.  
  - *Example:* `\inven`
- **`invnext` / `invprev`** (and `invnextp`, `invprevp`, `invnextw`, `invprevw`) — Cycle inventory selection across items, powerups, or weapons only.  
  - *Syntax:* `invnext`, `invprev`, `invnextp`, `invprevp`, `invnextw`, `invprevw`  
  - *Permissions:* Some variants require spectator/intermission access for menu navigation.  
  - *Example:* `\invnextw`
- **`invuse`** — Uses the currently selected item or activates the highlighted menu entry when a menu is open.  
  - *Syntax:* `invuse`  
  - *Permissions:* Usable while spectating or during intermission; flood-exempt.  
  - *Example:* `\invuse`
- **`use`**, **`use_only`**, **`use_index`**, **`use_index_only`** — Activates an item by name (including holdable shortcuts) or by inventory index, optionally suppressing weapon switches.  
  - *Syntax:* `use <item_name>` or `use_index <index>`; `_only` variants suppress weapon chains  
  - *Permissions:* Available to active players; flood-exempt for binds.  
  - *Example:* `\use holdable`
- **`weapnext` / `weapprev` / `weaplast`** — Cycle to the next, previous, or last-used weapon, honouring owned inventory and weapon usability.  
  - *Syntax:* `weapnext`, `weapprev`, `weaplast`  
  - *Permissions:* Available to active players; flood-exempt for smooth weapon binds.  
  - *Example:* `\weapprev`
- **`impulse`** — Provides Quake 1-style impulse shortcuts for weapon selection, cheats, and special actions (e.g., `9` gives all weapons when cheats are allowed).  
  - *Syntax:* `impulse <0..255>`  
  - *Permissions:* Available to active players (cheat-protected actions still respect server cheat gating).  
  - *Example:* `\impulse 10`
- **`hook`** / **`unhook`** — Fires or resets the grapple when grapple support is enabled.  
  - *Syntax:* `hook` / `unhook`  
  - *Permissions:* Available to active players; flood-exempt for quick grappling binds.  
  - *Example:* `\hook`
- **`kill`** — Self-destructs the player after spawn protection and cheat checks clear, counting as a suicide.  
  - *Syntax:* `kill`  
  - *Permissions:* Available to active players.  
  - *Example:* `\kill`
- **`wave`** — Performs gestures (point, wave, salute, taunt, flip-off) and pings teammates when pointing at map items or players.  
  - *Syntax:* `wave [0-4]` (defaults to flip-off; `1` point, `2` wave, `3` salute, `4` taunt)  
  - *Permissions:* Available to active players.  
  - *Example:* `\wave 1`

### Information, HUD, and analytics

- **`clientlist`** — Prints a sortable table of connected clients with IDs, skill rating, ping, and team data.  
  - *Syntax:* `clientlist [score|time|name]`  
  - *Permissions:* Usable while dead, spectating, or during intermission.  
  - *Example:* `\clientlist name`
- **`help`** — Shows the help computer in non-deathmatch games or falls back to the scoreboard in competitive modes.  
  - *Syntax:* `help`  
  - *Permissions:* Usable while dead or spectating; flood-exempt.  
  - *Example:* `\help`
- **`score`** — Toggles the multiplayer scoreboard, closing menus first when necessary.  
  - *Syntax:* `score`  
  - *Permissions:* Usable while dead, spectating, or during intermission; flood-exempt.  
  - *Example:* `\score`
- **`fm`** / **`kb`** — Toggle frag message popups or switch the kill beep sound set, cycling presets when no value is supplied.  
  - *Syntax:* `fm` | `kb [0-4]`  
  - *Permissions:* Usable while dead or spectating.  
  - *Example:* `\kb 3`
- **`mapinfo`** — Prints the current map’s filename, long name, and authorship metadata.  
  - *Syntax:* `mapinfo`  
  - *Permissions:* Usable while dead or spectating.  
  - *Example:* `\mapinfo`
- **`mappool`** / **`mapcycle`** — Lists maps from the pool or cycle, with optional string filtering, and reports totals.  
  - *Syntax:* `mappool [filter]` / `mapcycle [filter]`  
  - *Permissions:* Usable while dead or spectating.  
  - *Example:* `\mappool q2dm`
- **`motd`** — Displays the server Message of the Day if one is loaded.  
  - *Syntax:* `motd`  
  - *Permissions:* Usable while spectating or during intermission.  
  - *Example:* `\motd`
- **`mymap`** — Queues a personal map pick (with optional rule modifiers) when `g_maps_mymap` is enabled and the player is authenticated.  
  - *Syntax:* `mymap <mapname> [+flag] [-flag] ...`  
  - *Permissions:* Usable while dead or spectating.  
  - *Example:* `\mymap q2dm1 +pu`
- **`sr`** — Reports the player’s skill rating alongside the server average for the current gametype.  
  - *Syntax:* `sr`  
  - *Permissions:* Usable while dead or spectating.  
  - *Example:* `\sr`
- **`stats`** — Stubbed CTF stats dump (announces availability when CTF flags are active).  
  - *Syntax:* `stats`  
  - *Permissions:* Usable during intermission or as a spectator.  
  - *Example:* `\stats`

---

## Voting commands

- **`callvote`** / **`cv`** — Launches a vote if voting is enabled, enforcing warmup rules, per-player limits, and `g_vote_flags`. Lists available vote types when called with no arguments.  
  - *Syntax:* `callvote <command> [params]` (alias `cv`)  
  - *Permissions:* Usable while dead or spectating when the server allows spectator votes.  
  - *Example:* `\callvote map q2dm2`
- **`vote`** — Casts a yes/no ballot on the active vote, accepting shorthand `1`/`0` and preventing double voting.  
  - *Syntax:* `vote <yes|no>`  
  - *Permissions:* Usable while dead (live players only).  
  - *Example:* `\vote yes`

Enabled vote types and their validation logic (map, restart, shuffle, unlagged, cointoss, random, arena, etc.) are registered through `RegisterVoteCommand`, which enforces argument counts, gametype eligibility, and cooldowns before the vote menu appears. Consult the server host guide for the `g_vote_flags` matrix.

---

## Cheat & debug commands (development servers only)

These commands are guarded by `CheatProtect` and require cheats to be enabled via server settings. Use them on private or test servers.

- **`alert_all`** — Forces all monsters to target you immediately.  
  - *Syntax:* `alert_all`
  - *Example:* `\alert_all`
- **`check_poi`** — Reports whether the current Point of Interest is visible from your position using PVS tests.  
  - *Syntax:* `check_poi`
  - *Example:* `\check_poi`
- **`clear_ai_enemy`** — Sets an AI flag telling all monsters to forget their current enemy.  
  - *Syntax:* `clear_ai_enemy`
  - *Example:* `\clear_ai_enemy`
- **`give`** — Grants specific items, ammo, or the entire inventory when `all` is supplied; optional count supported for ammo-like items.  
  - *Syntax:* `give <item_name|all|health|...> [count]`
  - *Example:* `\give rocketlauncher`
- **`god`** / **`immortal`** — Toggles god mode or immortal mode flags, printing the resulting state.  
  - *Syntax:* `god` / `immortal`
  - *Example:* `\god`
- **`kill_ai`** — Removes all active monsters from the level.  
  - *Syntax:* `kill_ai`
  - *Example:* `\kill_ai`
- **`list_entities`** / **`list_monsters`** — Dump entity or monster tables (with positions for monsters) to the console.  
  - *Syntax:* `list_entities` / `list_monsters`
  - *Example:* `\list_monsters`
- **`noclip`**, **`notarget`**, **`novisible`** — Toggle collision, targeting, or visibility flags respectively, printing ON/OFF feedback.  
  - *Syntax:* `noclip` | `notarget` | `novisible`
  - *Example:* `\noclip`
- **`set_poi`** / **`check_poi`** — Sets or inspects the Point of Interest used by other tools.  
  - *Syntax:* `set_poi`
  - *Example:* `\set_poi`
- **`target`** — Fires all entities that match the supplied `targetname`, mimicking trigger relays.  
  - *Syntax:* `target <target_name>`
  - *Example:* `\target door_trigger`
- **`teleport`** — Warps the player to specified coordinates with optional pitch/yaw/roll overrides.  
  - *Syntax:* `teleport <x> <y> <z> [pitch] [yaw] [roll]`
  - *Example:* `\teleport 0 0 128`

---

## Quick cross-links

- Hosts: the **Admin Command Quick Reference** now links here for deeper coverage—pair it with the `g_vote_flags` presets in the [Server Host Guide](server-hosts.md).  
- Players: skim the [Voting and Match Etiquette](players.md#voting-and-match-etiquette) section after reviewing relevant player commands above.  
- Need more automation context? The programmers guide outlines how commands register with the dispatcher in `command_system.cpp`.

