# WORR vs. Quake II Rerelease — Reference Journal

## 1. Vision and Scope
- WORR positions itself as an "advanced gameplay expansion and server mod" that deliberately extends both single-player and multiplayer systems, citing vast entity support, competitive tooling, and UI polish beyond the base rerelease.
- The original rerelease source focuses on shipping the combined game DLL, API updates, and tooling guidance for modders rather than gameplay-layer overhauls, underscoring a much narrower remit.

## 2. Gameplay and Balance Extensions
- WORR tunes weapons (faster rockets, shorter Plasma Beam range, calmer Hunter/Vengeance spheres) and documents the changes for server operators. The stock rerelease retains original weapon values and lacks this balance changelog.
- Manual QA checklists capture behaviors unique to WORR, such as warmup deaths consuming lives in elimination modes and strict validation of vote arguments. These systems are not present or documented in the base game.

## 3. Multiplayer Modes and Match Flow
- WORR ships 18 competitive gametypes plus Practice Mode, from Domination and Clan Arena to ProBall and Gauntlet, and tags each with structured metadata (flags, spawn identifiers) for runtime logic. The rerelease DLL does not expose a comparable expanded roster.
- The match engine runs a full state machine (warmup, ready-up, countdown, live, overtime) with Marathon meta-progression that tracks leg scores across maps. This systemic layer is absent from the vanilla rerelease, which relies on simpler deathmatch loops.
- WORR persists ghosts for disconnected players, storing spawn origin/angles so returning clients respawn seamlessly. This is beyond the original game's session handling.

## 4. Map Rotation, Voting, and Match Configuration
- WORR replaces the rerelease's `g_map_list`/`g_map_list_shuffle` cvars with a JSON-driven map pool, MyMap queues, and post-match selectors governed by player counts, history, and map tags. The stock DLL's rotation is limited to parsing the `g_map_list` string at runtime.
- `g_vote_flags` exposes granular toggles for twelve vote types (maps, gametype, shuffle, arena changes, etc.), enabling curated call-vote menus that have no equivalent control surface upstream.

## 5. Administration and Server Operations
- WORR modularizes command handling into dedicated admin, client, cheat, system, and voting sources. Admin tooling covers ban/allow lists, arena forcing, ready-state mass toggles, and match control workflows absent from the stock command set.
- The rerelease retains the monolithic `g_cmds.cpp` with traditional Quake II console commands, underscoring how WORR expands administrative breadth rather than modifying the legacy command hub directly.

## 6. Player Experience and UI
- WORR augments the HUD renderer to respect spectator states, draw mini-score portraits, and format additional scoreboard data within the layout parser. The baseline rerelease renderer lacks these conditional paths and mini-score presentation tweaks.
- README highlights an adaptive HUD, mini-score displays, frag messaging, and announcer integration. These features go beyond the rerelease's default presentation layer.

## 7. Data, Persistence, and Ecosystem Support
- WORR writes structured match summaries (IDs, totals, per-player stats) to JSON to feed external analytics. These export surfaces are not implemented in the base DLL.
- Server-side client configs and ghost stats recording persist preferences and outcomes across reconnects, enabling continuity features the upstream project does not advertise.

## 8. Release Management and Repository Structure
- WORR formalizes release cadence into Stable/RC/Beta/Nightly channels, guiding operators through upgrade paths and support expectations. The base rerelease repository instead documents build requirements and API notes for mod developers.
- The repository keeps curated references (`refs/`), tooling (`tools/`), and documentation that expand on gameplay systems. This material is not bundled with the original source drop and underscores WORR's focus on long-term maintainability and knowledge sharing.
