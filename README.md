# CurrentSensor — STM32 USB current sensor concept

A work-in-progress current measurement circuit by Michael Cutler, started in November 2020. The KiCad schematic sketches a USB-C powered STM32F042K6T6 controller, a two-stage MAX4239 analogue front end, and an I²C connection labelled STEMMA QT.

**Status: schematic concept, not a fabrication-ready board.** This repository contains no PCB layout, Gerbers, assembly BOM, firmware, calibration procedure, or measured performance results. Component references remain unannotated, many footprints are unassigned, and range selection is still marked `TODO DT3T Switch? Jumpers?` in the schematic.

## View the design

- [Schematic PDF](CurrentSensor.pdf) — view the circuit without installing KiCad.
- [Schematic source](CurrentSensor.sch) — editable legacy Eeschema format.
- [KiCad project](CurrentSensor.pro) — legacy project settings.

The PDF identifies KiCad **5.1.7**. Open `CurrentSensor.pro` with the legacy KiCad toolchain, or import a copy into a newer KiCad release and review conversion results before saving. Modern KiCad compatibility and electrical rule checks have not been verified.

The schematic references `Makeristic-KiCad-Library:STM32F042K6T6`. Clone the [Makeristic KiCad Library](https://github.com/makeristic/Makeristic-KiCad-Library), register its legacy symbol library in KiCad, and install the standard KiCad libraries. No symbol cache or project-local library tables are included here; unresolved library references need to be resolved before editing or exporting.

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

These are design intentions visible in the schematic, not validated measurement ranges or interface capabilities. Range switching, the measurement connection to the controller, firmware, PCB layout and calibration remain unfinished. Review those before attempting a build.

## Related projects and contributions

Browse the [Makeristic project catalogue](https://github.com/makeristic/makeristic.github.io#readme) for the other boards, templates and Halloween badges.

Use [issues](https://github.com/makeristic/CurrentSensor/issues) for circuit questions or proposed improvements. Include the KiCad version, affected nets/components, and any simulation or measurement evidence. For a design PR, explain electrical changes and include an updated schematic PDF; keep automatic format migrations separate from circuit changes.

## Licence

Michael Cutler's original circuit design and documentation are available under the [MIT licence](LICENSE). Referenced KiCad libraries and linked manufacturers' datasheets retain their own terms; this licence does not relicense those third-party materials.
