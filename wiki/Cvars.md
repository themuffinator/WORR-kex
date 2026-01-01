# WORR Cvar Reference

This guide catalogs WORR’s server and gameplay cvars by responsibility. Defaults and flags originate from the registration logic in `g_main.cpp`; adjust settings via `set`/`seta` on the server console or config files. Update this page whenever new cvars land so operators and players can track behavior changes.

## Server Identity & Access Control
| Cvar | Default | Notes |
| --- | --- | --- |
| `hostname` | `"Welcome to WORR!"` | Advertised server name in browsers. |
| `password` | `""` | Player password; set to gate private lobbies. |
| `spectator_password` | `""` | Optional spectator-only password. |
| `admin_password` | `""` | Required for admin command authentication. |
| `needpass` | `0` | Auto-updated flag exposing whether passwords are active. |
| `filterban` | `1` | Ban list behavior (1=ban matches, 0=allow list). |

## Lobby Size & Warmup Flow
| Cvar | Default | Notes |
| --- | --- | --- |
| `maxclients` | `8` per split player constant | Latched engine limit; set at init. |
| `maxplayers` | `16` | Caps active player slots per match. |
| `minplayers` | `2` | Minimum participants before the match can start. |
| `match_start_no_humans` | `1` | Auto-start matches without humans after warmup grace. |
| `match_auto_join` | `1` | Auto-assigns connecting players to a team. |
| `match_crosshair_ids` | `1` | Displays player names under crosshair for team modes. |
| `warmup_enabled` | `1` | Enables warmup pre-game phase. |
| `warmup_do_ready_up` | `0` | Require players to `/ready` before countdown. |
| `g_warmup_countdown` | `10` | Seconds to count down once ready conditions met. |
| `g_warmup_ready_percentage` | `0.51` | Portion of players required to be ready. |

## Match Timing & Respawn Rules
| Cvar | Default | Notes |
| --- | --- | --- |
| `fraglimit` | `0` | Frags needed to end non-round matches. |
| `timelimit` | `0` | Minutes before auto-ending the match. |
| `roundlimit` | `8` | Rounds per match for elimination modes. |
| `roundtimelimit` | `2` | Minutes per round in elimination modes. |
| `capturelimit` | `8` | Flag captures to win CTF variants. |
| `mercylimit` | `0` | Score delta that triggers mercy end. |
| `match_do_force_respawn` | `1` | Force players to respawn automatically after death. |
| `match_force_respawn_time` | `2.4` | Seconds before auto respawn triggers. |
| `match_holdable_adrenaline` | `1` | Allows adrenaline to persist between deaths. |
| `match_instant_items` | `1` | Enables instant-use items from inventory. |
| `match_items_respawn_rate` | `1.0` | Multiplier for pickup respawn timers. |
| `match_do_overtime` | `120` | Seconds of overtime if tied at regulation end. |
| `match_powerup_drops` | `1` | Drop carried powerups on death. |
| `match_powerup_min_player_lock` | `0` | Minimum human players before powerups spawn. |
| `match_player_respawn_min_delay` | `1` | Minimum seconds before respawning players. |
| `match_player_respawn_min_distance` | `256` | Minimum units from enemies for respawns. |
| `match_timeout_length` | `120` | Duration of tactical pauses in seconds. |
| `match_weapons_stay` | `0` | Toggle Quake III style weapons-stay logic. |
| `match_drop_cmd_flags` | `7` | Bitmask controlling `/drop` command options. |

## Gametype & Modifier Controls
| Cvar | Default | Notes |
| --- | --- | --- |
| `g_gametype` | `1` (`ffa`) | Active gametype index/short name (`0` is Practice Mode for no-score warmups with self-damage disabled). |
| `deathmatch` | `1` | Enables deathmatch logic when true. |
| `teamplay` | `0` | Legacy toggle forced on for team modes. |
| `ctf` | `0` | Legacy toggle forced on for CTF variants. |
| `marathon` | `0` | Enables multi-map Marathon meta progression. |
| `g_marathon_timelimit` | `0` | Minutes per leg before forced advance. |
| `g_marathon_scorelimit` | `0` | Score delta per leg before advance. |
| `g_ruleset` | `RS_Q2` | Active ruleset (Q2, Q3A, custom). |
| `g_level_rulesets` | `0` | Allow BSP metadata to override rulesets. |
| `g_instaGib` | `0` | Instagib modifier (latched). |
| `g_quadhog` / `g_nadeFest` / `g_frenzy` | `0` | Additional match modifiers toggled at load. |
| `g_vampiric_damage` | `0` | Enables vampiric life steal; see supporting cvars for scaling. |
| `g_allow_techs` | `auto` | Governs tech pickups across modes. |
| `g_allow_grapple` | `auto` | Controls offhand grappling availability. |
| `g_allow_forfeit` | `1` | Allows teams to `/forfeit`. |
| `g_allow_kill` | `1` | Permit `/kill` command in lobbies. |
| `g_allow_mymap` | `1` | Enables player map queue feature. |
| `g_allow_voting` | `1` | Master toggle for callvote system. |
| `g_allow_vote_mid_game` | `0` | Permit votes while a match is live. |
| `g_allow_spec_vote` | `0` | Allow spectators to vote. |

## Map Rotation & Overrides
| Cvar | Default | Notes |
| --- | --- | --- |
| `g_maps_pool_file` | `"mapdb.json"` | JSON pool enumerating map metadata. |
| `g_maps_cycle_file` | `"mapcycle.txt"` | Text rotation consumed by `nextmap`. |
| `g_maps_selector` | `1` | Enable end-of-match selector vote. |
| `g_maps_mymap` | `1` | Allow MyMap queue submissions. |
| `g_maps_allow_custom_textures` | `1` | Permit custom texture assets for pool entries. |
| `g_maps_allow_custom_sounds` | `1` | Permit custom sound assets for pool entries. |
| `g_entity_override_dir` | `"maps"` | Directory containing entity override files. |
| `g_entity_override_load` | `1` | Load `.ent` overrides at runtime. |
| `g_entity_override_save` | `0` | Save `.ent` overrides produced in-editor. |
| `match_map_same_level` | `0` | Force Marathon legs to stay on current BSP when set. |

## Physics & Movement
| Cvar | Default | Notes |
| --- | --- | --- |
| `g_gravity` | `800` | Global gravity acceleration. |
| `g_max_velocity` | `2000` | Max player speed clamp. |
| `g_roll_speed` / `g_roll_angle` | `200` / `2` | View roll response. |
| `g_stop_speed` | `100` | Friction stop speed threshold. |
| `g_knockback_scale` | `1.0` | Global knockback multiplier. |
| `g_lag_compensation` | `1` | Enables unlagged hitscan compensation. |
| `g_instant_weapon_switch` | `0` | Latched instant weapon swapping. |
| `g_quick_weapon_switch` | `1` | Quick switch toggle (latched). |
| `g_weapon_respawn_time` | `30` | Weapon respawn seconds for non-arena modes. |
| `g_weapon_projection` | `0` | Enables weapon model projection offset. |

## Player Experience & Messaging
| Cvar | Default | Notes |
| --- | --- | --- |
| `g_frag_messages` | `1` | Toggles frag feed overlay. |
| `g_ghost_min_play_time` | `60` | Minimum real-time seconds required before saving a reconnect ghost slot. |
| `g_showmotd` / `g_showhelp` | `1` | Display MOTD/help prompts on connect. |
| `g_motd_filename` | `"motd.txt"` | MOTD file path relative to game dir. |
| `g_auto_screenshot_tool` | `0` | Enables automated intermission screenshots. |
| `g_owner_auto_join` | `0` | Auto-join lobby owner to teams. |
| `g_owner_push_scores` | `1` | Push match scores to lobby owner HUD. |
| `g_inactivity` | `120` | Seconds before AFK kick triggers. |
| `g_verbose` | `0` | Verbose console logging (entity spawn diagnostics). |

## Health, Armor, and Items
| Cvar | Default | Notes |
| --- | --- | --- |
| `g_starting_health` | `100` | Base health on spawn. |
| `g_starting_health_bonus` | `25` | Temporary bonus health on spawn. |
| `g_starting_armor` | `0` | Armor granted on spawn. |
| `g_start_items` | `""` | CSV list of starting items. |
| `g_powerups` toggles (`g_no_powerups`, `g_no_items`, `g_no_mines`, `g_no_spheres`, `g_mapspawn_no_bfg`, etc.) | `0` | Disable specific pickups globally. |
| `g_arena_starting_health` / `g_arena_starting_armor` | `200` | Round-based loadout values for Clan Arena modes. |
| `g_arena_self_dmg_armor` | `0` | Mitigate self-damage via armor in arenas. |
| `g_vampiric_percentile` | `0.67` | Fraction of damage converted to healing when vampiric mode active. |

## Voting & Administration
| Cvar | Default | Notes |
| --- | --- | --- |
| `g_allow_admin` | `1` | Enables admin login flow for console commands. |
| `g_vote_flags` | `8191` (all votes) | Bitmask enabling specific vote topics. |
| `g_vote_limit` | `3` | Votes per player each map. |
| `g_allow_spec_vote` | `0` | Permit spectators to initiate votes. |
| `g_allow_vote_mid_game` | `0` | Allow votes during active matches. |
| `g_allow_voting` | `1` | Master toggle; disable to remove callvote entirely. |

## Cooperative, Horde, and PvE
| Cvar | Default | Notes |
| --- | --- | --- |
| `g_coop_enable_lives` | `0` | Enable shared life pool in coop. |
| `g_coop_num_lives` | `2` | Lives per player when coop lives enabled. |
| `g_coop_squad_respawn` | `1` | Enable squad respawn mechanic. |
| `g_coop_player_collision` | `0` | Toggle friendly collision in coop. |
| `g_coop_instanced_items` | `1` | Instanced item pickups per player. |
| `g_horde_starting_wave` | `1` | Initial wave index for Horde mode. |
| `g_frozen_time` | `180` | Seconds a player stays frozen in Freeze Tag. |
| `g_lms_num_lives` | `4` | Lives in Last Man/Team Standing. |

## Bots & AI
| Cvar | Default | Notes |
| --- | --- | --- |
| `ai_allow_dm_spawn` | `0` | Allow AI to spawn in deathmatch. |
| `ai_damage_scale` | `1` | Damage multiplier applied to AI. |
| `ai_model_scale` | `0` | Model scale override for AI actors. |
| `ai_movement_disabled` | `0` | Disable AI pathing (debug). |
| `bot_name_prefix` | `"B|"` | Prefix applied to bot names. |
| `bot_debug_follow_actor` / `bot_debug_move_to_point` | `0` | Debug draws for bot navigation. |

## Analytics & Diagnostics
| Cvar | Default | Notes |
| --- | --- | --- |
| `g_matchstats` | `0` | Emit match summary JSON on completion. |
| `g_statex_enabled` | `1` | Enable stat export subsystem (StateX). |
| `g_statex_humans_present` | `1` | Require human players before exporting stats. |
| `g_owner_push_scores` | `1` | Broadcast scores to lobby host for integrations. |
| `g_auto_screenshot_tool` | `0` | Capture end-match screenshots for archives. |

## Legacy Movement & View
| Cvar | Default | Notes |
| --- | --- | --- |
| `run_pitch` / `run_roll` | `0.002` / `0.005` | Player view bob controls. |
| `bob_pitch` / `bob_roll` / `bob_up` | `0.002` / `0.002` / `0.005` | View bobbing intensities. |
| `gun_x`, `gun_y`, `gun_z` | `0` | Weapon model offsets in view space. |

## Miscellaneous
| Cvar | Default | Notes |
| --- | --- | --- |
| `g_disable_player_collision` | `0` | Disables player-player collision globally. |
| `g_item_bobbing` | `1` | Toggle idle item bob animations. |
| `g_fast_doors` | `1` | Speed multiplier for door movers. |
| `g_frames_per_frame` | `1` | Internal simulation tick multiplier (debug). |
| `g_friendly_fire_scale` | `1.0` | Scales friendly fire damage. |
| `g_showmotd` | `1` | Show MOTD at spawn. |
| `g_mapspawn_no_plasmabeam` / `g_mapspawn_no_bfg` | `0` | Disable specific weapons by map metadata. |
| `g_mover_debug` | `0` | Extra logging for movers. |
| `g_mover_speed_scale` | `1.0` | Multiply mover speeds for testing. |

For legacy compatibility, WORR still honors engine-provided cvars like `dedicated`, `cheats`, and `skill`; confirm their values before relying on behavior in game logic.
