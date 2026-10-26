# CurrentSensor source audit

26 October 2026. Scope: the complete legacy schematic/project/PDF, component definitions, dependencies, interfaces and available build artefacts. This is an unfinished circuit concept, with no PCB or executable firmware to test.

## Blocked on me

The circuit cannot be certified as electrically correct or ready to build. Range selection, amplifier supply/shutdown connections, controller measurement integration and component annotation need design work and validation. No fabricated board, test procedure or measured limits are available in the repository.

## Changed

- Restored `CurrentSensor-cache.lib` with the 20 referenced symbol definitions: 19 from the matching KiCad 5.1.7 libraries and the STM32F042 symbol from the existing Makeristic library. This fixes the reproduced `Failed to load schematic` error in the modern CLI. Drawings and pin definitions are preserved; the cache names expand library-qualified identifiers and aliases as the legacy loader expects.
- Added `sym-lib-table` using `${KIPRJMOD}` to locate the documented sibling library clone. No machine-specific absolute path is committed.
- Added the exact upstream KiCad licence and cache provenance/exclusions. The imported STM32 symbol's broader provenance remains incomplete; restoring the cache does not grant new third-party rights.
- Corrected the README to distinguish a successful load from an electrical check pass and to identify the unconnected amplifier pins.

## Found

### Electrical issues that remain

- **High — incomplete amplifier power/control:** both `MAX4239AUT` pin 5 shutdown inputs are unconnected at schematic coordinates `(6800,3300)` and `(8550,3300)`. The second amplifier's pin 6 positive supply at `(8450,2700)` is also unconnected. The pin identities are confirmed by the same-version KiCad definitions. Supply/control wiring is not inferred from nearby nets.
- **High — incomplete current path:** `R_SENSE_UA` and `R_SENSE_MA` positive terminals are unconnected, the amplifier input resistor has a dangling end, and the schematic explicitly asks `TODO DT3T Switch? Jumpers?`. There is no complete range-selection circuit.
- **High — no measurement integration:** the analogue output is not connected to a selected controller ADC input. No firmware, calibration or supported current/voltage range is supplied.
- **Important — references and footprints:** most components still have `?` references and many footprints are blank. The STM32 component has a wildcard footprint suggestion. Resolve annotation and exact package assignments before generating a BOM or PCB.
- **Important — prototype completeness:** SWD/UART labels are exposed only as schematic nets, with no programming/host connector implementation. The presence of USB and I²C net labels does not establish functioning firmware or validated interfaces.

### Checks performed

The original cache-free checkout reproduced the CLI load failure. A temporary cache assembled from the recorded library definitions made the same unchanged schematic load and enabled ERC. The final committed cache has the same definitions as that successful reproduction.

Run from the project directory, with a temporary KiCad configuration if isolation is needed:

```sh
kicad-cli-nightly sch erc --format json --output /tmp/CurrentSensor-erc.json CurrentSensor.sch
```

KiCad nightly **10.99.0** reported 110 violations in the isolated configuration:

- 13 errors: 6 unconnected pins, 5 undriven power pins and 2 undriven inputs.
- 97 warnings: 77 library-symbol configuration warnings, 9 footprint-library warnings, 4 isolated labels, 4 multiple-net-name warnings and 3 dangling wire endpoints.

These counts depend on configuration. Undriven power warnings can require source flags or circuit work; no flags or rule exclusions were added to conceal them. A netlist export warns about annotation and collapses duplicate references, so its component count is not valid design evidence.

Cache definitions were checked against the source libraries, including symbol identity, pins and drawing geometry. Project-table paths, local Markdown links and `git diff --check` were checked. The schematic/PDF are byte-for-byte unchanged.

No PCB DRC, firmware build, physical measurements, tolerance analysis, source/sink protection review, modern-format migration or manufacturing validation has been performed. The original work-in-progress status is retained.
