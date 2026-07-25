# Integrated WalkieTalkie schematic

This revision replaces the ESP32 DevKit, TP4056 breakout and MAX98357A
breakout with manufacturer-assembled components.

## Project files

- `WalkieTalkie.kicad_sch` — main/lower PCBA schematic.
- `WalkieTalkie_Front.kicad_sch` — front/user-interface PCBA schematic.
- `WalkieTalkie_JLCPCB.kicad_sym` — project symbol library imported from
  JLCPCB/EasyEDA part records.
- `WalkieTalkie_JLCPCB.pretty` — matching project footprints.
- `WalkieTalkie_JLCPCB.3dshapes` — imported 3D models.
- `JLCPCB_ASSEMBLY_PARTS.csv` — selected major assembly parts and LCSC IDs.

## Important design behavior

- The ESP32-WROOM-32U contains its own U.FL/IPEX antenna connector.
- USB-C VBUS feeds the TP4056 charger and the system load-sharing path.
- USB D+/D- feed a CH340C USB-to-UART bridge. This revision uses manual
  BOOT and RESET buttons instead of the more failure-prone auto-download
  transistor circuit.
- The TP4056 charge current is set near 500 mA with a 2.4 kOhm PROG resistor.
- DW01A + FS8205A provide single-cell protection.
- TPS63031 provides regulated 3.3 V across the normal single-cell range.
- MAX98357A runs from VSYS. Its two speaker pads are a bridge output; neither
  pad is ground.
- R20-R23 are fitted for the Black firmware mapping. R24-R27 are DNP.
  Reverse those two groups for the Grey mapping.

## Hand-soldered parts

The main schematic intentionally uses large plated solder-wire pads for:

- J4: two speaker wires.
- J5: three potentiometer wires.
- J6: two push-to-talk button wires.
- J7: two external status-LED wires.
- J8: two laser-module wires.

The five face buttons are SMD parts on the front PCB and are intended for
manufacturer assembly.

## Before ordering

The OLED part is wave-solder/high-difficulty and the INMP441 listing may
require Standard PCBA or pre-ordering into the JLCPCB private parts library.
Recheck stock and price when ordering. Confirm all imported footprints against
the current manufacturer datasheets before routing or production.

The older breakout-module PCB files and reports are preserved in
`Previous_Breakout_Draft`. Create fresh PCB files after setting the enclosure
dimensions.
