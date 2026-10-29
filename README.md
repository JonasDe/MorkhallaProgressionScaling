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
does anything in `ExcludedCreatures` (default: Moose, Jotun Witches and Barka). Health and damage stay vanilla. Raid
events are not changed at all.

Works alongside spawn and raid config mods: whatever they set is the base this mod multiplies,
and it never overwrites their values.

Group sizes and "how many at once" are rounded at random, so the average matches the multiplier:
at 1.5x a creature that normally comes alone shows up alone half the time and in a pair the other
half, instead of always in pairs.

## Configuration

### Where the settings are

The config file is created the first time you start the game with the mod installed:

```
BepInEx/config/com.jonasd.valheim.morkhallaprogressionscaling.cfg
```

- **Mod manager** (r2modman, Thunderstore Mod Manager, Gale): open your profile's config
  editor and pick `com.jonasd.valheim.morkhallaprogressionscaling`. No need to find the file.
- **By hand**: the `BepInEx` folder is in your Valheim folder, or in your mod manager profile
  folder. Open the file with any text editor.
- **Dedicated server**: edit the same file in the server's `BepInEx/config` folder.

Changes apply while the game or server runs: save the file and the mod reloads it within about
a second (a server then sends the new settings to every player). No restart needed.

### Format

Plain text: a `[Section]` heading, then one `Name = value` per line. Lines starting with `#` are
explanations and are ignored. Only change the value after the `=`.

```ini
[1 - Steps]
MaxSteps = 3
SpawnIncreasePerStep = 0.5
StarChancePerStep = 5
GammeltrollsPerStep = 1

[2 - General]
Enabled = true
ExcludedCreatures = Moose, JotunWitch, Barka
```

### Settings

| Section | Setting | Default | What it does |
| --- | --- | --- | --- |
| 1 - Steps | `MaxSteps` | 3 | Progression stops at this many cleared Morkhallas |
| 1 - Steps | `SpawnIncreasePerStep` | 0.5 | Added per step to Deep North spawning: 0.5 = +50% per step (1.5x, 2x, 2.5x) |
| 1 - Steps | `StarChancePerStep` | 5 | Percentage points of star chance added per step (vanilla is about 10%) |
| 1 - Steps | `GammeltrollsPerStep` | 1 | Gammeltrolls per step at each new invasion (1, 2, 3) |
| 2 - General | `Enabled` | true | Turns the mod on or off |
| 2 - General | `ExcludedCreatures` | Moose, JotunWitch, Barka | Creatures never scaled, comma separated prefab names |
| 2 - General | `LogDetails` | false | Writes what gets scaled to the BepInEx log, for testing |
| 3 - Gammeltrolls | `MinDistance` / `MaxDistance` | 15 / 30 | How far from the ice the Gammeltrolls are placed, in metres |

Set a value to `0` to turn that part off, e.g. `GammeltrollsPerStep = 0` for no Gammeltrolls.

### Examples

| You want | Change |
| --- | --- |
| A gentler curve (1.25x, 1.5x, 1.75x) | `SpawnIncreasePerStep = 0.25` |
| Brutal (2x, 3x, 4x) | `SpawnIncreasePerStep = 1` |
| More stars, same spawns | `StarChancePerStep = 10` |
| Only stars and Gammeltrolls | `SpawnIncreasePerStep = 0` |
| Keep growing past the third Morkhalla | `MaxSteps = 5` |

### Server or player?

On a server, **the server's settings apply to every player**: while connected, players' own
`MaxSteps`, `SpawnIncreasePerStep`, `StarChancePerStep`, `Enabled` and `ExcludedCreatures` are
ignored. Settings marked "Server only" in the file (everything about Gammeltrolls,
`CountedEvents`) are only read on the server. `LogDetails` is each player's own. In single player,
your own file is used.

## Multiplayer

Install on the server and on every player. The server keeps the step count and sends its settings
to all players, so everyone scales the same way.

To set the count by hand (for example on a world where Morkhallas were cleared before you
installed the mod), an admin can open the console with `devcommands` and type
`setkey mps_morkhallaclears 2`.
