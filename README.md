# Helix

Starter repository for the Helix industrial dual-extrusion platform.

## Current project docs
- Quotation-derived requirements: `docs/REQUIREMENTS.md`
- BOM: `docs/BOM.md`
- Flow/IO-Link integration notes: `docs/FLOW_AND_IOLINK.md`
- Klipper version and firmware repo strategy: `docs/KLIPPER_VERSION_AND_REPO.md`
- Klipper base config: `config/klipper/printer.cfg`

## Process focus
- Ambient-temperature dual-mass extrusion (no heated bed, no thermal extrusion loop).
- Optional flow sensor feedback.
- Optional IO-Link integration through an external bridge.
- Servo-controlled alginate valve for synchronized co-deposition.

## Platform requirements
- Operator workstation compatibility: Windows 10 and Windows 11.
- Klipper host runtime: Linux environment (CB1/CM4 class).

## Quick start
1. Complete final part numbers in `docs/BOM.md`.
2. Replace placeholders in `config/klipper/printer.cfg` with real pins and values.
3. Test valve macros and feeder direction with dry runs.
4. Add flow sensor validation and safety interlocks.
5. Pin a validated Klipper commit hash after commissioning.
