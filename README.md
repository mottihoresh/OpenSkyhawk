# A-4E Home Cockpit

DCS A-4E Skyhawk home cockpit build — physical panels and controls for the DCS mod.

## Goal
Develop panels and controls based on references from the sim and other sources. All functionality from the sim should be modeled.

## Repository Structure

```
A-4 Test/
├── CAD/                    # Fusion 360 source files (.f3d) and exports (.step, .stl)
│   ├── Center_Console/
│   ├── Left_Console/
│   ├── Right_Console/
│   └── Shared/             # Common hardware, brackets, mounting fixtures
│
├── PCB/                    # KiCad projects, one folder per board
│   ├── Center_Console/
│   ├── Left_Console/
│   ├── Right_Console/
│   └── Libraries/          # Shared KiCad symbols and footprints
│
├── Firmware/               # Arduino sketches
│   └── Libraries/          # Shared Arduino libraries
│
└── Docs/
    ├── References/         # Cockpit photos, manuals, screenshots
    └── Datasheets/         # Component datasheets
```

## Console Layout

| Console | Panels |
|---------|--------|
| Center Console | Armament, main flight instruments |
| Left Console | ECM, fuel, electrical systems |
| Right Console | Radios, nav |

## Hardware Notes

### Screw Standards
| Size | Use |
|------|-----|
| M2 | PCB mounts, small standoffs |
| M3 | Placards, light rings, small brackets |
| M4 | Instrument bezels, gauge mounting (clearance Ø4.3–4.5 mm) |
| M5 | Panel-to-subpanel, corner mounts (clearance Ø5.3–5.5 mm) |

### Switch Sizing
- Base toggle switches: 12 mm / ½″
- ECM module toggles: ~6 mm / ¼″

### Gauges
- Liquid Oxygen Gauge: 2-5/8″ (~67 mm total)
- Radar Altimeter: 3-1/8″ (~100 mm total with bezel)

## References
- [Open Hornet Hardware](https://github.com/jrsteensen/OpenHornet)
- [Open Hornet Software](https://github.com/jrsteensen/OpenHornet-Software)
- [The Warthog Project](https://thewarthogproject.com/)
- [Viperpits](https://www.viperpits.org/smf/index.php)
- [The Skyhawk Association — Cockpit](https://skyhawk.org/page/skyhawk-cockpit)
