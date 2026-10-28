# Morkhalla Progression Scaling

**Deep North not hard enough? Missing the Ashlands' relentless assaults? Look no further!**

This mod turns every cleared Morkhalla into another notch on the Deep North's difficulty dial. Break
the Malicious Ice, start a Jotunn invasion, and the frozen north answers: more creatures, bigger
packs, more stars, and Gammeltrolls waiting at the next invasion. A progression hardness tuner that
grows with you, one Morkhalla at a time.

## Steps

Progression works in **steps**: one step is one cleared Morkhalla. A Morkhalla counts as cleared
when you break the Malicious Ice at the bottom and the Jotunn invasion starts. The count is saved
with the world and stops at `MaxSteps` (3 by default, the three Morkhallas vanilla needs).

With the default settings:

| Steps | Deep North spawns | Star chance | Gammeltrolls at that invasion |
| --- | --- | --- | --- |
| 0 | vanilla | vanilla (about 10%) | - |
| 1 | 1.5x | +5 | 1 |
| 2 | 2x | +10 | 2 |
| 3 (max) | 2.5x | +15 | 3 |

## What scales

- **Day and night spawns**: Deep North creatures spawn more often, more of them can be around at
  once, and their groups are bigger.
- **Morkhalla**: dungeons you have not entered yet hold more creatures, spread evenly over the
  dungeon, and their respawning spawn areas allow more creatures at once.
- **Jotunn invasion**: more creatures spawn around the invasion.
- **Stars**: Deep North creatures that can have stars get them more often. Creatures without
  stars never get any.
- **Gammeltrolls**: each new invasion places Gammeltrolls near the ice, one per step so far. They
  spawn once, never respawn, and stay until killed.

Only hostile creatures are scaled: seals, fish and the invasion's meteors stay vanilla, and so
does anything in `ExcludedCreatures` (default: `Moose`). Health and damage stay vanilla. Raid
events are not changed at all.

Works alongside spawn and raid config mods: whatever they set is the base this mod multiplies,
and it never overwrites their values.

## Configuration

| Section | Setting | Default | What it does |
| --- | --- | --- | --- |
| Steps | MaxSteps | 3 | Progression stops at this many cleared Morkhallas |
| Steps | SpawnIncreasePerStep | 0.5 | +50% Deep North spawning per step |
| Steps | StarChancePerStep | 5 | +5 percentage points star chance per step |
| Steps | GammeltrollsPerStep | 1 | Gammeltrolls per step at each new invasion |
| General | Enabled | true | Turns the mod on or off |
| General | ExcludedCreatures | Moose | Creatures never scaled, comma separated |
| Gammeltrolls | MinDistance / MaxDistance | 15 / 30 | How far from the ice they are placed, in metres |

## Multiplayer

Install on the server and on every player. The server keeps the step count and sends its settings
to all players, so everyone scales the same way.

To set the count by hand (for example on a world where Morkhallas were cleared before you
installed the mod), an admin can open the console with `devcommands` and type
`setkey mps_morkhallaclears 2`.
