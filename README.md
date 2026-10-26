# CurrentSensor — STM32 USB current sensor concept

A work-in-progress current measurement circuit by Michael Cutler, started in November 2020. The KiCad schematic sketches a USB-C powered STM32F042K6T6 controller, a two-stage MAX4239 analogue front end, and an I²C connection labelled STEMMA QT.

**Status: schematic concept, not a fabrication-ready board.** This repository contains no PCB layout, Gerbers, assembly BOM, firmware, calibration procedure, or measured performance results. Component references remain unannotated, many footprints are unassigned, and range selection is still marked `TODO DT3T Switch? Jumpers?` in the schematic.

## View the design

- [Schematic PDF](CurrentSensor.pdf) — view the circuit without installing KiCad.
- [Schematic source](CurrentSensor.sch) — editable legacy Eeschema format.
- [KiCad project](CurrentSensor.pro) — legacy project settings.

The PDF identifies KiCad **5.1.7**. Open `CurrentSensor.pro` with the legacy KiCad toolchain, or import a copy into a newer KiCad release and review conversion results before saving. The source audit below checks loading and ERC with a modern nightly; no format migration or passing electrical validation is claimed.

The restored [symbol cache](CurrentSensor-cache.lib) contains the 20 symbol definitions used by the legacy schematic, allowing it to load without silently substituting different symbol geometry. The [project symbol table](sym-lib-table) resolves `Makeristic-KiCad-Library:STM32F042K6T6` from a sibling clone of the [Makeristic KiCad Library](https://github.com/makeristic/Makeristic-KiCad-Library). Install the standard KiCad libraries as well. See [cached symbol provenance](THIRD_PARTY_NOTICES.md) for source versions and reuse terms.

```sh
gh repo clone makeristic/CurrentSensor
gh repo clone makeristic/Makeristic-KiCad-Library
```

## Circuit outline

- USB-C USB 2.0 connector with 5.1 kΩ CC resistors, a Schottky diode, and USBLC6-2SC6 protection.
- HT7533-1 regulator for 3.3 V, with a filtered analogue supply.
- STM32F042K6T6 with USB, I²C, UART and SWD net labels.
- Two MAX4239AUT amplifier stages and an LMV321AS5X reference buffer.
- Candidate sense resistors of 10 kΩ, 10 Ω and 0.01 Ω, labelled for nA, µA and mA measurement respectively.
- A four-pin connector labelled STEMMA QT and I²C pull-ups.

These are design intentions visible in the schematic, not validated measurement ranges or interface capabilities. Range switching, the measurement connection to the controller, firmware, PCB layout and calibration remain unfinished. Both MAX4239 shutdown inputs are unconnected, and the second amplifier's positive supply is not wired. Review and complete the circuit before attempting a build.

## Source audit

The [source audit report](docs/code-audit-report.md) records the October 2026 inspection and exact limitations. KiCad nightly 10.99.0 loads the legacy source with the restored cache and runs ERC. The isolated check reports **13 errors and 97 warnings**; it is not an electrical validation pass. Most warnings concern library/footprint configuration, while the unconnected amplifier pins and incomplete sense path are actual circuit work.

Component references are still unannotated. Do not use a netlist exported from this state as manufacturing input: duplicate references prevent a complete component list. No circuit wiring or historical PDF has been changed by this audit.

## Related projects and contributions

Browse the [Makeristic project catalogue](https://github.com/makeristic/makeristic.github.io#readme) for the other boards, templates and Halloween badges.

Use [issues](https://github.com/makeristic/CurrentSensor/issues) for circuit questions or proposed improvements. Include the KiCad version, affected nets/components, and any simulation or measurement evidence. For a design PR, explain electrical changes and include an updated schematic PDF; keep automatic format migrations separate from circuit changes.

## Licence

Michael Cutler's original circuit design and documentation are available under the [MIT licence](LICENSE). Cached/reference library definitions and linked manufacturers' datasheets retain their own terms; this licence does not relicense those third-party materials. See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) and [LICENSE-KiCad.md](LICENSE-KiCad.md).
