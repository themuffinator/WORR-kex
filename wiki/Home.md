# WORR Knowledge Base

Welcome! This is the home page for the WORR wiki and the fastest way to find the right guide for your role.

> **Maintainers:** `docs/wiki/` is the canonical in-repo knowledge base. The `wiki/` folder mirrors it for the GitHub-hosted wiki, so keep both in sync and push updates to the separate `WORR-kex.wiki` repository.

## Start Here

| Persona | Focus |
| --- | --- |
| [Server Hosts](Server-Hosts.md) | Deployment workflows, map rotation tooling, vote governance, analytics exports. |
| [Players](Players.md) | Gametype rules, combat changes, UI improvements, etiquette for votes and reconnects. |
| [Level Designers](Level-Design.md) | Entity catalogue, map metadata schema, spawn naming, gametype-specific considerations. |
| [Programmers](Programmers.md) | Repository layout, build tooling, subsystem entry points, contribution workflow. |

Additional reference pages:
- [Monsters Manual](Monsters.md) - Full roster with attacks, behaviors, and counterplay tips.
- [Gametypes and Modifiers Manual](Gametypes-and-Modifiers.md) - Detailed rules and match modifiers for every mode.
- [Console Commands](Commands.md) - Administrative, competitive, and player-facing console verbs.
- [Cvar Reference](Cvars.md) - Tunable runtime settings grouped by responsibility.
- [Gameplay Balance Changes](Gameplay-Balance.md) - Weapon, item, and powerup tuning compared to stock Quake II.
- [Spawn Point Manual](Spawn-Points.md) - Multiplayer spawn selection, respawn timing, and map setup tips.
- [Tournament Format Guide](Tournaments.md) - Match sets, roster locks, and map veto workflow.

## Highlights

- **18 competitive gametypes plus a practice format** for no-score warmups.
- **Map system depth** with JSON pools, MyMap queues, and post-match selectors.
- **Admin control** via vote flags, match management commands, and lockouts.
- **Player continuity** with adaptive HUD cues and ghost persistence on reconnects.

## Getting Oriented

- **Why WORR?** Review the [comparison journal](../docs/worr_vs_quake2.md) for a high-level breakdown of how WORR evolves the rerelease DLL's gameplay, administration, and analytics stack.
- **Release cadence:** Consult [Versioning & Release Channels](../docs/versioning.md) for stability expectations before upgrading production servers.
- **What changed recently?** Track packaged updates and patch notes in [`CHANGELOG.md`](../CHANGELOG.md) once published.

## Contributing to Documentation
1. Edit the relevant Markdown under `docs/wiki/` and mirror it into `wiki/`.
2. Run `markdownlint` (if available locally) to keep formatting consistent.
3. Commit the change in the main repository.
4. Clone `https://github.com/themuffinator/WORR-kex.wiki.git` and copy the updated pages across (or add the wiki repository as a secondary remote).
5. Push to publish the live wiki.

Pull requests that modify gameplay, commands, or configuration should update the corresponding wiki page so downstream operators and players can adopt the change confidently.
