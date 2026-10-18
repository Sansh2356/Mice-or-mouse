A603EP Mouse Clone - KiCad project
==================================
KiCad 7 format; opens in KiCad 7, 8 and 9 (newer versions offer to upgrade - click Yes).

Files
- A603EP_Mouse.kicad_pro        Project - open this
- A603EP_Mouse.kicad_sch        Schematic traced from board HYC-343-1
- A603EP_Mouse.kicad_pcb        PCB: outline, wheel slot, cable notch, chip/LED window, 8 holes,
                                and every part placed at its original position (not yet routed)
- A603EP_Mouse.kicad_sym / .pretty   Project symbols and footprints
- A603EP_PCB_fit_test.pdf       1:1 print to check the board against the original and the shell
- A603EP_Mouse_schematic.pdf    Printable schematic

How it was made
- Chip footprint: 1.778 mm pitch, 14.0 mm row spacing (confirmed by your paper test, option B).
- Everything else measured from your straight-down photo of the green side, using the chip pads
  as the ruler. Board comes out 38.9 x 66.4 mm (your ruler: 40 x 65). Accuracy about +-0.3 mm.
- KiCad's netlist and the PCB pad nets match the schematic exactly.

CHECKS - ALL DONE (19 Oct 2026)
- 1:1 fit test passed on the original board and in the shell.
- Encoder common = front outer leg; + = left leg for LED1, C1, D1-D4 ('+' marked on silkscreen); SW6 has 2 legs.
- Micro-switches: middle leg = common (pin 1), front = normally-open (pin 2), back = normally-closed (unused).

THEN ROUTE
- Route on one side (B.Cu) like the original if you want to etch at home, or use both sides
  if a fab makes it. Keep C2 close to U1 pins 10/11 and the USB tracks short.
- Run Inspect > Design Rules Checker. Order 1.6 mm thickness.
