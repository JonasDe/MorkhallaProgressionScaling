# Changelog

## 0.1.1

- README: where the config file is, how to edit it, its format, every setting, example presets,
  and which settings the server decides for everyone. No gameplay changes.

## 0.1.0

- First release. Every cleared Morkhalla is a step (counted when its ice starts a Jotunn
  invasion), up to `MaxSteps` (3).
- Each step adds `SpawnIncreasePerStep` (+50%) to Deep North spawning: day and night spawns
  (rate, amount, group size), Morkhalla creatures and Jotunn invasion creatures.
- Each step adds `StarChancePerStep` (+5 points) to the star chance of Deep North creatures that
  can have stars.
- Each new Jotunn invasion places Gammeltrolls nearby, one per step (1, 2, 3). They spawn once and
  never respawn.
- Raid events and other mods' spawn settings are left alone. The server's settings apply to all
  players.
