## Bom for Extruder Suports:
- Filament: ABS or ASA
- Heat Inserts(voron specs) x2
- M3x20 x2 Cap Screws for securing the extruder support on the toolhead
  - For Sherpa Mini:
    - M3x18  x2 Cap Screws - for securing the extruder on the extruder support
    - M3x25  x2 Cap Screws - for securing the extruder on the extruder support with the filament cutter addon
  - For Orbiter v2
    - M3x14  x2 Cap Screws - for securing the extruder on the extruder support
    - M3x20  x2 Cap Screws - for securing the extruder on the extruder support with the filament cutter addon

## Toolboards Supports

You can use the toolboarts supports that I providet here or you can use whatever toolboards supports you can find online that apply to the Sherpa Mini and Orbiterv2
## BOM:
- Filament: ABS or ASA
- Heat Insert(voron specs) x2
- M3x8  x2 for securing the toolboard support on the extruder
- M3x10  x2 for securing the toolboard
- Spacer  x2 between the extruder and extruder support. the lenght for this spacers depends on what size(length) motors you have. I prefer metalic ones.

## Links:
- Spacers - https://de.aliexpress.com/item/1005006251587333.html - or - https://de.aliexpress.com/item/1005003493226449.html

## Filament Cutter Addon

The Filament Cutter Addon is ment for use in regular non toolchanger setups, with or without an MMU of some sort. I do not recomend using with a toolchanger settup, the pin interlocking system between the shuttle and backplate is not ment for such shocks.

# BOM for Filament Cutter Adaptor:

- Filament: ABS or ASA
- M3x6 x1
- M3 Nut x1
- M3x35 x2pcs
- 2 springs from a balpoint pen
- Blade x1
- 4mm OD x 2mm ID  metalic tubing
- 3mmx10mm pin

# Printing:

4 walls, 5 tops and bottoms, 40-50 infill.

# Links:

- Blade - https://www.amazon.de/dp/B0CXCX7GPG?ref=ppx_yo2ov_dt_b_fed_asin_title&th=1
- Metal Tubbing - https://de.aliexpress.com/item/1005005681927768.html
- Nylon washers(optional) - https://de.aliexpress.com/item/33004939470.html

# Assembly:

Guide yourself from the pictures. The M3x35 screws must be with half lenght thread. If you have with full lenght thread you will need to use the nylon washers I linked above, or the spring will get caught on the screw threads and will get pulled in the hole of the blade holder and jam the hole thing. You will need to adjust how much the long screws are screwed in the printed part so that the blade will sit close to the filament. The 3mm pin is used so that when cutting the blade should not burry herself into the printed part due the blade being angled. The small piece of metal tubing is necesary so that the blade should have something to cut against. You can use a PTFE tubing for that, but I think the PTFE tubing will crack over time. The tubing should be flush on the blade side and go on the extruder exit port as long as needet. The PTFE tubing from the hotend should end flush on top of the extruder adapter printed part, and should be chamfered to aid the filament entry.

# The Pusher.

The Pusher is a piece of plastic that holds an M5 screw. Its uset to push the Filament Cutter cutting lever(blade holder) against and cut the filament. The M5 screw must be adjusted so that when the toolhead is in position in front of the M5 screw ready to do the cutting, the distance between the M5 screw and the cutting lever should be about 0.5-1mm.

# BOM for Pusher

- Filament: ABS or ASA
- M3x12 x2
- M3 Hammerhead T-Nut x2
- M5x20 Screw

# Printing:

4 walls, 5 tops and bottoms, 40-50 infill.

# Macro:

```
[gcode_macro CUT_FILAMENT_AND_UNLOAD]
description: Cut and Unload filament
gcode:
    M109 S230
    G92 E0                # Zero the extruder
    G1 E-30 F1000
    FILAMENT_CUT
    G90
    G1 X175 Y50 Z100 F8000
    G92 E0                # Zero the extruder
    G1 E-100 F500
    G92 E0                # Zero the extruder
#    M104 S0               # Turn-off hotend

[gcode_macro FILAMENT_CUT]
description: Cut The Filament
# you must set the x pos in front of the pusher
# the distance between the pusher and the cutting lever(blade holder) should be arround 0.5-1mm when toolhead is in position in front of the pusher befor cutting. adjust the Pusher M5 screw accordingly
gcode:
    G90
    G1 X271 Y{printer.configfile.settings.stepper_y.position_max-4} F15000    # move toolhead in position befor cutting
    G1 Y{printer.configfile.settings.stepper_y.position_max}                  # cut
    G1 Y{printer.configfile.settings.stepper_y.position_max-10} F15000        # move away
```


The FILAMENT_CUT macro does only the cut move. The CUT_FILAMENT_AND_UNLOAD macro will heat up the nozzle, retract a small amount of filament, activate the FILAMENT_CUT macro and move the toolhead in the front of the printer, then unload the rest of the filament. Feel free to modify those macro at will.

