# Cached symbol provenance

`CurrentSensor-cache.lib` restores the symbol definitions needed to load this legacy schematic without changing component placement, wiring, pin numbers or circuit intent. It is reference/library material, excluded from the original-work MIT grant in `LICENSE`.

- Nineteen standard definitions come from the [KiCad symbol libraries, tag 5.1.7](https://github.com/KiCad/kicad-symbols/tree/5.1.7), matching the version identified by the original schematic PDF. Source libraries are `Amplifier_Operational`, `Connector`, `Device`, `Power_Protection`, `Regulator_Linear`, `Switch` and `power`. Aliases are expanded under the cache names expected by the legacy schematic.
- The `STM32F042K6T6` definition comes from the [Makeristic KiCad Library](https://github.com/makeristic/Makeristic-KiCad-Library/blob/56d55dbcb78e53db3f9bb6471a92d703b4260f02/Makeristic-KiCad-Library.lib). Its pin definitions, drawings and imported source metadata are preserved. That collection does not have complete per-asset licensing provenance; this cache does not create a new licence grant for the imported symbol.

The standard KiCad definitions retain **CC BY-SA 4.0 with the KiCad library exception**. See [LICENSE-KiCad.md](LICENSE-KiCad.md), copied from the upstream 5.1.7 revision, and the [KiCad library licence explanation](https://www.kicad.org/libraries/license/). No vendor or imported library material is relicensed as MIT.
