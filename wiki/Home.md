# WORR Knowledge Base

Welcome! This is the home page for the WORR wiki and the fastest way to find the right guide for your role.

> **Maintainers:** The Markdown in `wiki/` is the source for the GitHub-hosted wiki. Mirror updates from this folder into the [`WORR-kex` wiki](https://github.com/themuffinator/WORR-kex/wiki) by pushing to the separate `WORR-kex.wiki` repository.

## Start Here

| Persona | Focus |
| --- | --- |
| [Server Hosts](Server-Hosts.md) | Deployment workflows, map rotation tooling, vote governance, analytics exports. |
| [Players](Players.md) | Gametype rules, combat changes, UI improvements, etiquette for votes and reconnects. |
| [Level Designers](Level-Design.md) | Entity catalogue, map metadata schema, spawn naming, gametype-specific considerations. |
| [Programmers](Programmers.md) | Repository layout, build tooling, subsystem entry points, contribution workflow. |

Additional reference pages:
- [Console Commands](Commands.md) - Administrative, competitive, and player-facing console verbs.
- [Cvar Reference](Cvars.md) - Tunable runtime settings grouped by responsibility.

## Highlights

- **18 competitive gametypes plus Practice Mode**, including no-score warmups with self-damage disabled.
- **Map system depth** with JSON pools, MyMap queues, and post-match selectors.
- **Admin control** via vote flags, match management commands, and lockouts.
- **Player continuity** with adaptive HUD cues and ghost persistence on reconnects.

## Getting Oriented

- **Why WORR?** Review the [comparison journal](../docs/worr_vs_quake2.md) for a high-level breakdown of how WORR evolves the rerelease DLL's gameplay, administration, and analytics stack.
- **Release cadence:** Consult [Versioning & Release Channels](../docs/versioning.md) for stability expectations before upgrading production servers.
- **What changed recently?** Track packaged updates and patch notes in [`CHANGELOG.md`](../CHANGELOG.md) once published.

## Contributing to Documentation
1. Edit the relevant Markdown under `wiki/`.
2. Run `markdownlint` (if available locally) to keep formatting consistent.
3. Commit the change in the main repository.
4. Clone `https://github.com/themuffinator/WORR-kex.wiki.git` and copy the updated pages across (or add the wiki repository as a secondary remote).
5. Push to publish the live wiki.

Pull requests that modify gameplay, commands, or configuration should update the corresponding wiki page so downstream operators and players can adopt the change confidently.
