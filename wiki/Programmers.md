# Programmer Onboarding Guide

Welcome to WORR’s gameplay codebase. This guide highlights the repository structure, subsystem entry points, and workflow expectations so you can ship features without breaking the competitive ecosystem.

## Repository Tour
- `src/` contains the gameplay DLL with modular subsystems for match flow, commands, analytics, and UI. Each folder maps to a gameplay domain (e.g., `match/`, `gameplay/`, `commands/`).
- `docs/` captures balance notes, map system specs, analytics schemas, and comparative research to guide design decisions.
- `tools/` and `refs/` provide automation scripts and upstream source drops that inform regression fixes.

## Build & Branch Workflow
- Follow the branch naming conventions (`feature/*`, `hotfix/*`, `release/x.y`) and ensure the CI workflow passes before merging.
- Tag releases with semantic versions (`vMAJOR.MINOR.PATCH`) and update `CHANGELOG.md` for user-facing changes.
- Run the cross-platform CI locally when possible; GitHub Actions validates builds, tests, and packaging for each pull request.

## Key Gameplay Systems
- **Match State Machine:** `src/server/match/match_state.cpp` orchestrates warmup, ready-up, countdown, in-progress, overtime, and intermission transitions. Marathon meta-series logic lives here as well.
- **Gametype Registry:** `GAME_MODES` in `g_local.hpp` defines every supported gametype, short/long names, spawn identifiers, and flag metadata used for filtering entities and UI labels.
- **Client Allocation:** Use the helpers described in `docs/client_allocation.md` and declared in `g_clients.hpp` to manage `gclient_t` lifetime when adjusting `maxclients` or save/load flows.
- **Command Framework:** Commands register via `RegisterCommand` inside `src/server/commands/*`. Admin, client, cheat, and voting modules keep responsibilities isolated and feed into the wiki command reference.
- **Analytics Pipeline:** Match summaries land in JSON as documented in `docs/match_stats_json.md`; integrate new stats by updating both the serializer and documentation.

## Configuration & Rulesets
- Core cvars live in `g_main.cpp`. Group changes by responsibility (match pacing, map rotation, access control) and update the [Cvar Reference](Cvars.md) when you add or deprecate settings.
- Use `g_ruleset` and `g_level_rulesets` to auto-apply Quake II, Quake III, or custom rule profiles when loading BSP metadata. Entity filters rely on `ruleset` strings as described in the level design toolkit.

## Testing & QA Hooks
- Manual QA scenarios under `docs/manual_qa_*.md` describe behavior to validate before shipping elimination or voting tweaks.
- Enable `g_verbose` and `developer 1` while iterating so entity inhibition and rule transitions print helpful diagnostics.

## Analytics & Telemetry
- `g_matchstats` toggles JSON dumps; coordinate schema changes with analytics consumers and document new fields.
- Ghost and reconnect state uses persisted spawn data; adjust serialization carefully to avoid regressions in reconnection flows.

## Further Reading
- [WORR vs. Quake II Rerelease](../docs/worr_vs_quake2.md) - design intent and architectural comparisons.
- Persona guides for [Server Hosts](Server-Hosts.md), [Players](Players.md), and [Level Designers](Level-Design.md) to understand cross-disciplinary expectations.
