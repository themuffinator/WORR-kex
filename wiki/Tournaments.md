# Tournament Format Guide

Tournament is a match format built for organized play. In tournaments, a match is the full best-of set of games; outside tournaments, a match is just the single game on one map.

## What Tournament Mode Adds
- Best-of match sets (BO3/BO5/BO7/BO9) with automatic series scoring; outputs a combined JSON and HTML report after the final game.
- Participants locked to social IDs; non-participants stay in spectator and the `team` command is disabled.
- Home/away assignment, team names, and team captains (team-based modes) with turn-based map veto.
- Ready-up enforcement: veto and match start only after every participant is connected and ready.
- Map system lockdown: voting, MyMap, map selector, and duel queue are disabled while the tournament is active.
- Disconnect safety: if a participant drops during live play, the server triggers a timeout to allow reconnection.

## Quick Start for Hosts
1. Copy `tourney.json` into your active gamedir (for example `baseq2/`) or your mod folder.
2. Set `g_tourney_cfg` to the filename you want to load (defaults to `tourney.json`).
3. Open the Match Setup menu. If the config validates, "Tournament" appears as a format.
4. Select Tournament; the menu closes and the config is executed immediately.
5. Have all participants connect and ready up; once everyone is ready the veto menu pops for the home side.
6. Finish picks/bans and the match plays through the map order; "Map Choices" appears in the join menu after veto.

## Configuration File Overview
Tournament configs are JSON objects. The `match` object, `participants` array, and `mapPool` array are required.

### Root keys
- `name` (string, optional): Human-friendly label for announcements and reports.
- `seriesId` (string, optional): Custom series identifier for stats output. If omitted, the server generates one.
- `match` (object, required): Match setup and best-of settings.
- `teams` (object, optional): Team names and captains for team-based modes.
- `home` (string, optional): "red"/"blue" for team modes, or a participant social ID for FFA/duel. Defaults to the first participant (or their team).
- `away` (string, optional): "red"/"blue" for team modes, or a participant social ID for FFA/duel. Defaults to the opposing team or next participant.
- `participants` (array, required): Locked roster entries by social ID.
- `mapPool` (array, required): BSP names available for veto and picks. `map_pool` is also accepted.

### match
- `gametype` (string, required): Short name used by the `gametype` command (for example `duel`, `tdm`, `ctf`).
- `length` (string, optional): `short`, `standard`, `long`, or `endurance`. Default is `standard`.
- `type` (string, optional): `casual`, `standard`, `competitive`, or `tournament`. Default is `tournament`.
- `modifier` (string, optional): `standard`, `instagib`, `vampiric`, `frenzy`, or `gravity_lotto`. Default is `standard`.
- `bestOf` (string or integer, optional): `bo3`, `bo5`, `bo7`, `bo9` or `3`, `5`, `7`, `9`. Defaults to `bo3`.
- `maxPlayers` (integer, optional): Overrides `maxplayers` for the series.

### teams (team-based modes only)
- `red.name` / `blue.name` (string, optional): Team display names.
- `red.captain` / `blue.captain` (string, optional): Social IDs for captains. If omitted, the first participant with `captain: true` on that team becomes captain.

### participants
Each entry requires an `id` (social ID). Optional keys:
- `name` (string): Display name for reporting.
- `team` (string): `red` or `blue` for team modes; `free`/`ffa` for FFA or duel formats.
- `captain` (boolean): Marks the participant as the team captain if one is not already set.

Team-based tournaments require all participants to be locked to red or blue, and both teams must have a captain.

### home and away
- Team modes: use `red`/`blue`, or a participant social ID to infer the team.
- Free-for-all/duel: use participant social IDs only.
- If omitted, the first participant becomes home and the opposing team or next participant becomes away.

### mapPool
- Array of BSP names (for example `q2dm1`).
- Must contain at least `bestOf` entries.
- Duplicate names are ignored; keep the list clean.
- The server does not verify the map exists until it tries to load it, so make sure the content is installed.

## Example Configuration
```json
{
  "name": "WORR Weekly Cup",
  "seriesId": "weekly_cup_01",
  "match": {
    "gametype": "tdm",
    "length": "standard",
    "type": "tournament",
    "modifier": "standard",
    "bestOf": "bo3",
    "maxPlayers": 8
  },
  "teams": {
    "red": { "name": "Torch", "captain": "EOS:11111111111111111111111111111111" },
    "blue": { "name": "Frost", "captain": "EOS:22222222222222222222222222222222" }
  },
  "home": "red",
  "away": "blue",
  "participants": [
    { "id": "EOS:11111111111111111111111111111111", "name": "Aria", "team": "red", "captain": true },
    { "id": "EOS:33333333333333333333333333333333", "name": "Bram", "team": "red" },
    { "id": "EOS:22222222222222222222222222222222", "name": "Nox", "team": "blue", "captain": true },
    { "id": "EOS:44444444444444444444444444444444", "name": "Vale", "team": "blue" }
  ],
  "mapPool": ["q2dm1", "q2dm2", "q2dm3", "q2dm8"]
}
```

## Map Veto Flow
- The veto starts once all participants are connected and ready.
- Home picks or bans first via a pop-up menu, then away, then home, and so on.
- Picks stop once `bestOf - 1` maps are selected; bans only remain available while enough maps are left to finish picks.
- The decider game is chosen at random from the remaining pool; if nothing remains, a random map is chosen from the full pool.
- Captains (or the home/away players in FFA) can still use `tourney_pick <map>` or `tourney_ban <map>` if they prefer the console.
- Use `tourney_status` to see the pool, picks, bans, and whose turn is next.

## Match Flow and Safeguards
- Tournament matches always require ready-up. Every participant must be connected and marked ready before veto or match start.
- Team changes are locked to the roster. Non-participants are forced to spectator, and the join menu hides join/spectate actions.
- The join menu adds "Information" and unlocks "Map Choices" once veto completes.
- Voting, map selector, MyMap, and duel queue features are disabled while a tournament is active.
- If a participant disconnects during live play and `match_timeoutLength` is set, the server triggers a timeout and resumes automatically once everyone has reconnected.

## Replay a Game
Admins can replay a specific game if something goes wrong mid-series:
- Console: `replay <game#> confirm`
- Menu: Admin > Replay Game, then confirm the selection.

## Series Outputs
Each game still writes its normal match stats. When the match ends, WORR writes a combined report to:
- `baseq2/matches/series_<seriesId>.json`
- `baseq2/matches/series_<seriesId>.html`

## Troubleshooting
- If "Tournament" does not appear in the Match Setup menu, the config could not be found or parsed. Check the server console for the error.
- `g_tourney_cfg` is resolved from the active gamedir or `baseq2`. Keep filenames simple and avoid path separators.
- If the veto menu never appears, confirm all participants are ready and that home/away and captain IDs are valid.

For command syntax details, see the [Command Reference](Commands.md). Cvar defaults and scope are in the [Cvar Reference](Cvars.md).
