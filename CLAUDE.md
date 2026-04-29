# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

OpenSkyhawk is a physical DCS A-4E Skyhawk home cockpit build. It produces 3D-printed panels, custom PCBs, and Arduino firmware to replicate the full A-4E cockpit for use with the DCS A-4E Community Mod.

## Repository Structure

Organized by discipline, then by console position (Left / Center / Right):

- `CAD/` — Fusion 360 source files (`.f3d`). STLs and STEP exports are gitignored; generate from source.
- `PCB/` — KiCad projects, one subfolder per board. `PCB/Libraries/` holds shared symbols and footprints.
- `Firmware/` — Arduino sketches. Each subfolder is one physical controller (Arduino Pro Mini). `Firmware/Libraries/` holds shared code used across controllers.
- `Docs/References/` — cockpit photos, manuals, screenshots. `Docs/Datasheets/` — component datasheets.

## Firmware Architecture

Each folder under `Firmware/` maps to one Arduino Pro Mini (or compatible). A controller may drive one panel or a group of adjacent panels depending on I/O count.

- Port expansion via MCP23017 (I²C, up to 8 per bus at addresses 0x20–0x27, 16 GPIO each)
- DCS communication via [DCS-BIOS](https://github.com/dcs-bios/dcs-bios) — include as a library, do not modify
- Firmware is licensed GPL v2 (see `Firmware/LICENSE`) due to DCS-BIOS dependency

Naming convention: start as `Controller_01`, `Controller_02`, etc. Rename to reflect panel assignment once known (e.g. `Left_ECM`, `Center_Armament`).

## Licensing

| Layer | License |
|---|---|
| CAD, PCB, Docs | CC BY-NC-SA 4.0 (root `LICENSE`) |
| Firmware | GPL v2 (`Firmware/LICENSE`) |

## Hardware Standards

| Screw | Use |
|---|---|
| M2 | PCB mounts, small standoffs |
| M3 | Placards, light rings, small brackets |
| M4 | Instrument bezels, gauge mounts — clearance Ø4.3–4.5 mm |
| M5 | Panel-to-subpanel, corner mounts — clearance Ø5.3–5.5 mm |

- Toggle switches: 12 mm (standard), ~6 mm (ECM modules)
- LOX gauge: 2-5/8″ (~67 mm total)
- Radar Altimeter gauge: 3-1/8″ (~100 mm with bezel)

## KiCad CLI

Path: `/Applications/KiCad/KiCad.app/Contents/MacOS/kicad-cli` (v10.0.1)

Key commands:
```bash
KICAD=/Applications/KiCad/KiCad.app/Contents/MacOS/kicad-cli

# Validation
$KICAD pcb drc --output drc.json <board.kicad_pcb>
$KICAD sch erc --output erc.json <schematic.kicad_sch>

# Fabrication
$KICAD pcb export gerbers --output ./gerbers/ <board.kicad_pcb>
$KICAD pcb export drill --output ./gerbers/ <board.kicad_pcb>
$KICAD sch export bom --output bom.csv <schematic.kicad_sch>

# Fusion 360 fit check
$KICAD pcb export step --output board.step <board.kicad_pcb>

# Panel cutout template
$KICAD pcb export dxf --output cutout.dxf <board.kicad_pcb>

# Documentation
$KICAD sch export pdf --output schematic.pdf <schematic.kicad_sch>
```

## MCP Servers Available

- **Autodesk Fusion** — can read, execute, and update Fusion 360 designs directly
- **Notion** — all project notes live under the "A-4E Home Cockpit" page (Notion ID: `301575ac53b180b6a1b7cce9ba40ac79`), including a Panels database tracking status per panel

## Git

- Remote: `git@github.com:mottihoresh/OpenSkyhawk.git`
- Do not add `Co-Authored-By:` trailers to commits
- STLs, Gerbers, and other generated outputs are gitignored — commit sources only
