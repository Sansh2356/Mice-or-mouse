# A603EP Mouse Clone – progress snapshot (19 Oct 2026)

## Goal
Clone the wired mouse board HYC-343-1 (2023/5/5) on a new PCB, reusing the A603EP chip
(Instant Microelectronics, 12-pin single-chip USB optical sensor). The original chip appears dead,
so a working A603EP must be harvested from a same-model mouse.

## Done
- Full circuit traced with multimeter (see A603EP_traced_circuit.xlsx and the schematic).
- KiCad schematic built; KiCad netlist verified against the tracing (19 nets).
- Chip footprint confirmed by paper test: pitch 1.778 mm (leg 1–6 = 8.89 mm), rows 14.0 mm, body 10 x 12 mm.
- Board measured from photos, calibrated on the chip pads: 38.9 x 66.4 mm (ruler: 40 x 65), 1.5 mm thick -> order 1.6 mm.
- PCB laid out: outline, wheel slot, cable notch, chip/LED window, 8 holes, all parts at original positions.
  PCB pad nets match schematic (0 mismatches). 1:1 fit test PASSED on board and shell.
- Decisions: board made by a PCB maker (2 layers allowed); user routes tracks by hand.

## Key circuit facts
| Chip pin | Name | Connects to |
|---|---|---|
| 1 / 2 | DP / DM | USB D+ (orange) / D− (green) |
| 3 / 4 / 7 | R2 / R1 / R0 | button scan inputs |
| 5 / 6 | ZA / ZB | encoder outputs |
| 8 | LED | R1 680 Ω → tracking LED cathode |
| 9 | S1 | second button column |
| 10 | GND | USB G (white wire) |
| 11 | VDD5 | USB +5V (blue wire) |
| 12 | bLED | R2 100 Ω → D1–D4 cathodes |

Button matrix: R0 = left click (GND) / side 2 (S1); R1 = middle (GND) / side 1 (S1); R2 = right (GND) / DPI K6 (S1).
Encoder common → +5V (NOT GND). C1 47 µF and C2 100 nF across +5V/GND. Micro-switches: middle leg = common,
front leg = normally-open, back leg = normally-closed (unused).

## Checks (confirmed 19 Oct 2026)
1. Encoder: first (front, wheel-end) outer leg = common -> +5V. Matches the board.
2. Polarity: + = LEFT leg (top view) for tracking LED, C1, D1-D4. Matches the board; '+' marks added to silkscreen.
3. DPI button SW6: 2 legs. Matches the board.
=> Design is ready for routing.

## Next steps
2. Board Setup: clearance 0.2 mm, min track 0.25 mm, via 0.6/0.3 mm; net class Power (+5V, GND) 0.6 mm tracks, Default 0.3 mm.
3. Route: USB D+/D− first, C2 at pins 10/11, power, then buttons/encoder/LEDs. Prefer B.Cu. Optional GND pour.
4. Inspect > DRC: 0 errors, 0 unconnected. Send screenshots for review.
5. Fabrication outputs (Gerbers + drill), order 1.6 mm. Source working A603EP (same-model mouse).
6. Assemble, check +5V/GND short, test (detection, buttons, scroll direction, DPI).

## Files
- A603EP_Mouse.kicad_pro / _sch / _pcb, .kicad_sym, .pretty – KiCad project (KiCad 7 format)
- A603EP_PCB_fit_test.pdf, A603EP_Mouse_schematic.pdf, A603EP_traced_circuit.xlsx
- tools/ – scripts used to generate the schematic and PCB (for regenerating after changes)

## Backup option
ADNS-2700 (Avago, full datasheet, lens ADNS-5100-001) quoted by Anlinkda at $0.98; MX8733D (Sigma Micro, LCSC C2908844).
