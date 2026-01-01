# Programmers Guide

This guide orients engineers to WORR's codebase layout, workflows, and core gameplay systems so you can extend the mod without breaking its competitive backbone.

## Repository layout & primary subsystems

| Area | What lives here | Key references |
| --- | --- | --- |
| `src/server/` | Core gameplay module, including the consolidated gametype registry, match-state enums, and level-scoped data tracked during a session. | Start with `src/server/g_local.hpp` for top-level enums/structs and `src/server/match/` for runtime controllers like `match_state.cpp`. |
| `src/server/match/` | State machine governing warmup, countdown, live play, and leg transitions. Handles gametype switches and Marathon carry-over logic. | `match_state.cpp` orchestrates lifecycle helpers; supporting utilities live in the same folder. |
| `src/server/gameplay/` | Gameplay helpers such as spawn logic and client config persistence, including ghost-aware respawn paths. | Pair these with the `LevelLocals` ghost array in `g_local.hpp`. |
| `docs/` | System design notes, analytics schemas, mode rules, and host guidance. Essential when exposing data externally or aligning with persona-focused docs. | Use these specs to keep documentation synchronized with feature behavior. |
| `tools/` | Automation for CI, asset prep, and release engineering, backing the workflows described below. | See `tools/ci/run_tests.py` for local CI parity and `tools/release/` scripts for versioning chores. |
| `refs/` | Vendored upstream drops and historical notes that document deviations from vanilla Quake II rerelease sources. | Consult when reconciling behavior with upstream expectations. |

## Workflow expectations

- **Branches.** Follow the Git-flow-inspired names: `feature/<short-description>` for enhancements, `hotfix/<issue-or-bug-id>` for urgent fixes off `main`, and `release/x.y` to stage a new minor release.
- **CI contract.** Every PR must pass the `CI` GitHub Actions build that compiles on Windows/Linux, regenerates headers, runs tests, and uploads artifacts. Local smoke testing should mirror this using `tools/ci/run_tests.py` to compile and execute the standalone C++ test corpus.
- **Map config guardrails.** The sanitization helper now has explicit coverage for empty inputs, traversal/device specifiers, path separators, and other illegal characters via `tests/test_map_config_filename_sanitization.cpp`; exercise it locally with `python3 tools/ci/run_tests.py` before shipping related changes.
- **Release automation.** Tag releases on `main` using semantic versioning so `.github/workflows/release.yml` can package builds. Scripts like `tools/release/bump_version.py` and `tools/release/gen_version_header.py` keep `VERSION` and `version_autogen.hpp` aligned before tagging.
- **Hotfix cadence.** Ship hotfixes from `main`, merge them back into `develop` and any active `release/*` branch immediately, and rerun the required checks after resolving conflicts.
- **PR readiness.** Keep changes focused, update docs and changelog entries, add tests for behavioral shifts, and ensure CI passes (or document the exception) before requesting review.

## Gameplay systems to know

- **Gametype registry.** `GAME_MODES` centralizes metadata for every supported mode (short names, flags, spawn identifiers), while inline helpers in `Game` expose type/flag checks for other subsystems. This replaces parallel arrays and ensures new modes surface uniformly across UI, spawn logic, and voting.
- **Match state tracking.** `MatchState`, `WarmupState`, and `RoundState` enumerations, along with timers and counters on `LevelLocals`, describe the lifecycle of a match, including warmup gating, round sequencing, and overtime bookkeeping. Runtime transitions live in `src/server/match/match_state.cpp`, which also carries Marathon leg data forward between maps.
- **Ghost & analytics infrastructure.** Disconnect ghosts persist spawn origins/angles and pending respawn flags, while save hooks write ghost stats back through the client config layer. Post-match analytics serialize structured JSON (match IDs, totals, per-player arrays) for downstream tooling, so keep payload changes compatible with `docs/match_stats_json.md`.

## Client allocation helpers

The game module manually manages `gclient_t` storage; always use `AllocateClientArray`, `FreeClientArray`, or `ReplaceClientArray` from `src/server/gameplay/g_clients.hpp` so constructors, lag buffers, and global counters stay synchronized. The helpers are required during initial startup and when loading save games, and `ConstructClients`/`DestroyClients` are available for custom lifetimes.

## Further reading

- Exhaustive mapping of spawnable entities, items, and spawnflags: [Level Design Entity Catalogue](level-design.md#entity-catalogue).
- Side-by-side feature deltas versus the stock rerelease: [docs/worr_vs_quake2.md](../worr_vs_quake2.md).
- Server-facing configuration defaults: [Cvar Reference](cvars.md).
- Persona guides for cross-discipline context: server hosts, players, and level designers are indexed alongside this guide in the wiki landing page.
