# WORR Monster Manual

WORR ships with a blended roster: Quake II base monsters, mission pack additions, and a curated Quake 1 crossover lineup. This manual covers every spawnable monster and monster-class entity, with the classnames you need for map placement or admin spawning.

## How to use this guide
- Classname(s) list the entity names used in maps, spawners, and scripts.
- Profile summarizes movement type and combat role.
- Attacks call out the signature weapons or abilities.
- Counterplay offers quick, practical tips for players.

## Core Quake II roster

### Soldier Guards
- Classname(s): `monster_soldier_light`, `monster_soldier`, `monster_soldier_ss`
- Profile: Basic guard troopers with low to medium durability.
- Attacks: Light Guard uses a blaster, Machinegun Guard uses bullet bursts, Shotgun Guard hits hardest up close.
- Counterplay: Use cover, avoid close range vs shotgun, and keep moving to disrupt blind fire.

### Infantry
- Classname(s): `monster_infantry`
- Profile: Mobile mid-tier shooter that likes to run and gun.
- Attacks: Sustained machinegun bursts and a close-range kick.
- Counterplay: Strafe through bursts and punish when it stops to shoot.

### Gunner
- Classname(s): `monster_gunner`
- Profile: Heavy suppression unit that anchors a lane.
- Attacks: Chaingun bullet streams and arcing grenades.
- Counterplay: Break line of sight and avoid holding tight corners.

### Berserker
- Classname(s): `monster_berserk`
- Profile: Melee bruiser that closes distance fast.
- Attacks: Double punches, hammer slams, and jump strikes.
- Counterplay: Keep mid range and punish the recovery after big swings.

### Mutant
- Classname(s): `monster_mutant`
- Profile: Aggressive melee hunter with long leaps.
- Attacks: Slashing claws and lunging jumps.
- Counterplay: Backpedal and sidestep to avoid the leap arc.

### Gladiator
- Classname(s): `monster_gladiator`, `monster_gladb`
- Profile: Armored elite with strong mid to long range pressure.
- Attacks: Railgun shots and plasma style bursts plus a heavy melee smash.
- Counterplay: Use cover to break line of sight and rush during reload windows.

### Arachnid
- Classname(s): `monster_arachnid`
- Profile: Spider walker that plays as a sniper.
- Attacks: Railgun blasts with a clear windup.
- Counterplay: Stay mobile and deny long sightlines.

### Guardian
- Classname(s): `monster_guardian`
- Profile: Big bipedal bruiser with mixed melee and beam pressure.
- Attacks: Rapid blaster spin, laser beam, and a kick.
- Counterplay: Strafe the beam and keep hard cover between volleys.

### Gunner Commander
- Classname(s): `monster_guncmdr`
- Profile: Command variant with heavier ranged options.
- Attacks: Flechette volleys, grenade lobs, and ion ripper discs.
- Counterplay: Keep lateral movement and avoid mid range crossfire.

### Medic
- Classname(s): `monster_medic`, `monster_medic_commander`
- Profile: Support unit that keeps fights going.
- Attacks: Blaster or hyperblaster fire plus a healing cable.
- Special: Revives fallen monsters and can call reinforcements.
- Counterplay: Focus fire the medic first and finish corpses quickly.

### Parasite
- Classname(s): `monster_parasite`
- Profile: Close range drain specialist.
- Attacks: Proboscis tether that drains health while pulling targets in.
- Counterplay: Keep distance and break line of sight to interrupt the drain.

### Brain
- Classname(s): `monster_brain`
- Profile: Slow heavy with brutal mid range tools.
- Attacks: Tentacle lash, tongue strike, and dual beam shots.
- Counterplay: Circle strafe and punish during beam recovery.

### Iron Maiden
- Classname(s): `monster_chick`, `monster_chick_heat`
- Profile: Heavy rocket trooper.
- Attacks: Rocket barrages; heat variant uses tracking rockets.
- Counterplay: Keep moving and use cover to cut tracking.

### Floater (Technician)
- Classname(s): `monster_floater`
- Profile: Floating mid-range caster.
- Attacks: Blaster shots and a swinging melee strike.
- Counterplay: Track its vertical movement and keep strafing.

### Hover (Icarus)
- Classname(s): `monster_hover`, `monster_daedalus`
- Profile: Agile flying bot that patrols open space.
- Attacks: Blaster and heavier energy bursts.
- Counterplay: Stay under cover and punish when it lines up a shot.

### Flyer
- Classname(s): `monster_flyer`
- Profile: Light flying skirmisher.
- Attacks: Blaster bursts and short swoops.
- Counterplay: Keep aim discipline and pick them off early.

### Flipper
- Classname(s): `monster_flipper`
- Profile: Water-only shark that hunts in packs.
- Attacks: High speed bite and chase.
- Counterplay: Use vertical separation in water or avoid extended swims.

### Eel
- Classname(s): `monster_eel`
- Profile: Water-only ambusher with a zap.
- Attacks: Lightning discharge at close to mid range.
- Counterplay: Keep distance and use fast hitscan where possible.

### Tank
- Classname(s): `monster_tank`, `monster_tank_commander`
- Profile: Heavy armored walker built for area denial.
- Attacks: Blaster shots, machinegun spray, and rockets.
- Special: Tank Commander is tougher and uses heat-seeking rockets.
- Counterplay: Keep cover between you and the machinegun and dodge rocket volleys.

### Super Tank
- Classname(s): `monster_supertank`, `monster_boss5`
- Profile: Boss-tier heavy with multi-weapon pressure.
- Attacks: Rockets, grenades, machinegun, and heat beam bursts.
- Counterplay: Fight from cover and avoid stacked teammates.

### Hornet
- Classname(s): `monster_boss2`
- Profile: Flying boss that dominates open arenas.
- Attacks: Chaingun or hyperblaster streams plus rocket salvos.
- Counterplay: Stay near cover and keep lateral movement.

### Jorg
- Classname(s): `monster_jorg`
- Profile: Massive mech that punishes clustered players.
- Attacks: BFG blasts and heavy machinegun fire.
- Counterplay: Break line of sight when the BFG charge starts.

### Makron
- Classname(s): `monster_makron`
- Profile: End boss with mixed ranged options.
- Attacks: BFG shots, railgun hits, and blaster bursts.
- Counterplay: Keep moving and use cover to avoid railgun lanes.

## Mission pack additions

### Advanced Guards
- Classname(s): `monster_soldier_hypergun`, `monster_soldier_lasergun`, `monster_soldier_ripper`
- Profile: Up-armored guards that push more aggressive damage.
- Attacks: Hyperblaster bursts, blue laser volleys, and ion ripper discs.
- Counterplay: Treat them as high priority and avoid open lanes.

### Fixbot
- Classname(s): `monster_fixbot`
- Profile: Repair drone that supports allies and scripted objects.
- Attacks: Welding beam for repairs and a blaster when threatened.
- Special: Can heal or revive nearby monsters if allowed by spawnflags.
- Counterplay: Remove it early so it cannot stabilize the fight.

### Gekk
- Classname(s): `monster_gekk`
- Profile: Fast predator that punishes isolation.
- Attacks: Claw swipes, bite, acid spit, and leap tackles.
- Counterplay: Keep space and avoid getting cornered.

### Stalker
- Classname(s): `monster_stalker`
- Profile: Agile striker that can spawn from ceilings.
- Attacks: Blaster2 bolts and fast melee slashes.
- Counterplay: Check overhead routes and keep a close range weapon ready.

### Carrier
- Classname(s): `monster_carrier`
- Profile: Flying boss and reinforcement platform.
- Attacks: Rockets, grenades, railgun shots, and spawned flyers or kamikaze.
- Counterplay: Focus it to stop the reinforcements and keep moving.

### Widow
- Classname(s): `monster_widow`
- Profile: Grounded boss that controls space.
- Attacks: Blaster2 bursts and railgun shots.
- Special: Spawns Stalkers as reinforcements.
- Counterplay: Clear the adds and deny clean railgun lines.

### Widow2
- Classname(s): `monster_widow2`
- Profile: Beam-focused boss with heavy area control.
- Attacks: Heatbeam sweeps and disruptor shots.
- Special: Spawns Stalkers as reinforcements.
- Counterplay: Break line of sight during beam sweeps.

### Kamikaze
- Classname(s): `monster_kamikaze`
- Profile: Suicide flyer designed to trade damage.
- Attacks: Self-detonation on contact or when blocked.
- Counterplay: Shoot at range and avoid tight choke points.

## Quake and mission pack crossover roster

### Grunt
- Classname(s): `monster_army`
- Profile: Shotgun trooper with quick reaction time.
- Attacks: Shotgun blasts and short-range swings.
- Counterplay: Keep distance and strafe to reduce pellet hits.

### Enforcer
- Classname(s): `monster_enforcer`
- Profile: Energy infantry with solid mid-range pressure.
- Attacks: Blue energy blaster bolts.
- Counterplay: Keep moving and punish after volleys.

### Rottweiler
- Classname(s): `monster_dog`
- Profile: Fast melee hunter.
- Attacks: Rapid bite chain.
- Counterplay: Backpedal and use splash to stop charges.

### Rotfish
- Classname(s): `monster_fish`
- Profile: Water-only bite threat.
- Attacks: Rapid melee bites.
- Counterplay: Keep vertical separation or avoid long swims.

### Ogre
- Classname(s): `monster_ogre`, `monster_ogre_marksman`, `monster_ogre_multigrenade`
- Profile: Grenade specialist with brutal melee.
- Attacks: Grenade launcher and chainsaw swipes.
- Special: Marksman favors longer range lobs, Multigrenade fires spread volleys.
- Counterplay: Keep moving to dodge grenades and punish after lobs.

### Centroid
- Classname(s): `monster_centroid`
- Profile: Mechanical scorpion with ranged bursts.
- Attacks: Flechette volleys and tail stabs.
- Counterplay: Keep distance and dodge its jumpy dodges.

### Fiend
- Classname(s): `monster_demon1`
- Profile: Leap-heavy melee predator.
- Attacks: High damage jump slams and claws.
- Counterplay: Strafe the leap and punish on landing.

### Zombie
- Classname(s): `monster_zombie`
- Profile: Slow, stubborn thrower.
- Attacks: Explosive gib projectiles.
- Counterplay: Keep distance and finish with gib damage when possible.

### Spawn
- Classname(s): `monster_tarbaby`, `monster_tarbaby_hell`
- Profile: Hopping blob that multiplies.
- Attacks: Body slams and splashy impacts.
- Special: Splits into smaller spawns on death; hell variant is more aggressive.
- Counterplay: Clear the small spawns quickly to avoid swarms.

### Spike Mines
- Classname(s): `monster_spike`, `monster_spike_hell`, `monster_mine`, `monster_mine_hell`
- Profile: Floating proximity mines.
- Attacks: Detonate when close or on contact.
- Special: Hell variants hit harder.
- Counterplay: Pick them off from range before they close.

### Vore
- Classname(s): `monster_shalrath`
- Profile: Mid-range artillery caster.
- Attacks: Homing pods that track targets.
- Counterplay: Use cover and keep moving to break tracking.

### Knight
- Classname(s): `monster_knight`
- Profile: Melee swordsman with quick charges.
- Attacks: Heavy sword slashes and rush attacks.
- Counterplay: Keep range and punish between swings.

### Hell Knight
- Classname(s): `monster_hell_knight`
- Profile: Elite melee with ranged magic.
- Attacks: Flame spike volleys and crushing melee.
- Counterplay: Strafe the volley and avoid being cornered.

### Scrag
- Classname(s): `monster_wizard`
- Profile: Floating caster that kites.
- Attacks: Green acid bolts.
- Counterplay: Track vertical movement and keep hitscan ready.

### Shambler
- Classname(s): `monster_shambler`
- Profile: Heavy bruiser with brutal reach.
- Attacks: Lightning beam and massive melee swings.
- Counterplay: Use cover to break the beam and avoid close trades.

### Sword
- Classname(s): `monster_sword`
- Profile: Flying melee blade.
- Attacks: Fast slashing passes.
- Counterplay: Keep it at range and track its quick strafes.

### Shub-Niggurath
- Classname(s): `monster_oldone`
- Profile: Stationary boss that commands the arena.
- Attacks: Spawns reinforcements on a cadence.
- Counterplay: Clear adds quickly and focus damage between spawn cycles.

### Chthon
- Classname(s): `monster_chthon`, `monster_boss`
- Profile: Immobile lava boss.
- Attacks: Lava ball volleys from fixed positions.
- Special: Designed to be damaged by `target_chthon_lightning`.
- Counterplay: Trigger lightning strikes and avoid standing in lava arcs.

### Lavaman
- Classname(s): `monster_lavaman`
- Profile: Chthon variant with faster lava pressure.
- Attacks: Lava projectiles from a fixed stance.
- Counterplay: Use cover and avoid predictable lanes.

### Dragon
- Classname(s): `monster_dragon`
- Profile: Flying heavyweight with sustained fire.
- Attacks: Plasma and lava fireballs plus close range swipes.
- Counterplay: Keep moving vertically and punish during windups.

### Wyvern
- Classname(s): `monster_wyvern`
- Profile: Fast flying terror that controls mid range.
- Attacks: Flame bursts and lava balls.
- Counterplay: Deny hover space and stay mobile.

## Automated defenses and set pieces

### Turret
- Classname(s): `monster_turret`
- Profile: Stationary gun platform.
- Attacks: Blaster, machinegun, or rockets selected via spawnflags.
- Counterplay: Flank to avoid its firing arc and use cover.

### Commander Body
- Classname(s): `monster_commander_body`
- Profile: Static commander corpse for scripted scenes.
- Attacks: None.
- Notes: Cosmetic set piece used in intros and story beats.

### Tank Stand
- Classname(s): `monster_tank_stand`
- Profile: Set piece that cycles animation.
- Attacks: None until triggered.
- Notes: Teleports away when targeted (N64 behavior).

### Makron Stand
- Classname(s): `monster_boss3_stand`
- Profile: Stationary Makron platform stage.
- Attacks: None until scripted.
- Notes: Used for boss staging and intro sequences.
