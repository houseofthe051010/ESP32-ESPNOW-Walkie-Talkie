# Converting the two schematics into PCBs

Create a fresh PCB for each schematic. Do not reuse the archived breakout-board
layouts because their footprints and power architecture are different.

## Main board

1. Open `WalkieTalkie.kicad_pro`, then open `WalkieTalkie.kicad_sch`.
2. Run **Inspect > Electrical Rules Checker**. The imported EasyEDA symbols use
   `Unspecified` pin types, so KiCad reports `pin_to_pin` warnings. Check for
   actual red errors rather than automatically excluding everything.
3. Open **Tools > Assign Footprints**. Confirm every project-library footprint
   resolves through `WalkieTalkie_JLCPCB.pretty`.
4. Select **Tools > Update PCB from Schematic** or press **F8**.
5. When KiCad asks for a board, create and save a new
   `WalkieTalkie_Main.kicad_pcb`.
6. Draw the measured casing outline on `Edge.Cuts`. Add mounting holes, USB-C
   opening, U.FL access, battery clearance and cable-clearance areas before
   placing electrical parts.
7. Place the mechanical parts first: USB-C, ESP32/U.FL edge, battery connector,
   FFC connector and J4-J8 solder pads. Then place regulators and decoupling
   parts tightly around their ICs.

## Front board

1. Open `WalkieTalkie_Front.kicad_pro`, then
   `WalkieTalkie_Front.kicad_sch`.
2. Press **F8** and save a new `WalkieTalkie_Front.kicad_pcb`.
3. Draw the front-board outline from the casing.
4. Enter the exact button-center coordinates, OLED viewing-window location and
   microphone opening before placing the remaining parts.
5. Put a board cutout/acoustic hole directly under the INMP441 port. Verify the
   imported microphone footprint and its pin-1 orientation against the current
   datasheet.

## Routing rules

- Prefer four layers: front signals/components, solid ground, power, rear
  signals/components.
- Route USB D+/D- as a short, length-matched 90-ohm differential pair. Use the
  impedance dimensions supplied by the PCB manufacturer.
- Keep TPS63031 input/output capacitors and inductor beside U7. Minimize both
  switching-current loops.
- Route battery, VSYS and speaker paths with wide copper. Neither MAX98357A
  speaker output is ground.
- Use a solid ground plane beneath the ESP32 module, but keep antenna coax and
  the external antenna away from switching and speaker-current paths.
- Put thermal/ground vias in the TP4056, TPS63031 and MAX98357A exposed pads as
  required by their datasheets.
- Keep I2S traces short and referenced to continuous ground.

## Final checks and JLCPCB files

1. Run **Inspect > Design Rules Checker** until there are no shorts, clearance
   errors, unconnected nets or invalid board-edge errors.
2. Inspect both boards in the 3D Viewer. Confirm connector direction, FFC
   contact side, OLED orientation, button height and enclosure clearances.
3. Generate Gerbers and drill files from **File > Fabrication Outputs**.
4. Generate the component position file for both boards. JLCPCB usually expects
   reference, X, Y, layer and rotation fields.
5. Export a BOM containing the schematic `LCSC` field. Use
   `JLCPCB_ASSEMBLY_PARTS.csv` as the selected-part reference.
6. Recheck JLCPCB stock before ordering. The OLED and INMP441 may require
   Standard PCBA, pre-ordering or a manually sourced substitute.
