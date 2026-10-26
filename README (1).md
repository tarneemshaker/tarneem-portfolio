# G-Code Toolpath Generator & Analyzer

A small Python CLI tool for CNC machining, built to practice programmatic
G-code generation and parsing.

## What it does

**1. Generate** — Creates G-code for a rectangular pocket milling
operation: a raster (zig-zag) toolpath, cut in multiple depth passes,
from simple parameters (width, height, depth, tool diameter, stepover,
feed rate).

**2. Analyze** — Reads any existing G-code file and reports:
- Total rapid (G0) travel distance
- Total feed (G1/G2/G3) travel distance
- Number of tool changes
- Estimated machining time (based on feed rates in the file)

## Why I built it

To understand what CAM software is actually generating under the hood,
and to practice using Python (regex + basic geometry) to both produce and
interpret G-code rather than only using it through a machine controller.

## Usage

```bash
# Generate G-code for a 40x20x6mm pocket with a 6mm end mill
python gcode_toolpath_tool.py generate \
    --width 40 --height 20 --depth 6 \
    --tool-diameter 6 --stepover 0.5 \
    --feed 300 --plunge-rate 100 \
    --output pocket.nc

# Analyze any G-code file (including the one just generated)
python gcode_toolpath_tool.py analyze pocket.nc
```

## Example output

```
G-code analysis: pocket.nc
----------------------------------------
Lines parsed:            48
Rapid (G0) travel:       78.24 mm
Feed (G1/2/3) travel:    681.0 mm
Tool changes:            0
Estimated machine time:  2.47 min
----------------------------------------
```