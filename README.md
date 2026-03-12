# Helix

Starter repository for the Helix industrial dual-extrusion platform.

## Current project docs
- Quotation-derived requirements: `docs/REQUIREMENTS.md`
- BOM: `docs/BOM.md`
- Flow/IO-Link integration notes: `docs/FLOW_AND_IOLINK.md`
- Remote connectivity and camera architecture: `docs/REMOTE_CONNECTIVITY_AND_CAMERA.md`
- Electrical panel and safety concept: `docs/ELECTRICAL_PANEL_AND_SAFETY.md`
- Klipper version and firmware repo strategy: `docs/KLIPPER_VERSION_AND_REPO.md`
- Klipper base config: `config/klipper/printer.cfg`
- Klipper panel input example: `config/klipper/panel_inputs.cfg.example`
- Camera config example: `config/camera/crowsnest.conf.example`\n- OrcaSlicer future templates: `config/slicer/orcaslicer/`
- Panel IO mapping: `config/electrical/panel_io_map.csv`
- Commissioning checklist: `docs/COMMISSIONING_CHECKLIST.md`
- Procurement shortlist (public, no prices): `docs/PROCUREMENT_COMPONENT_SHORTLIST.md`

## Linked upstream firmware repos (submodules)
- `external/manta-m8p` -> `https://github.com/bigtreetech/Manta-M8P`
- `external/klipper` -> `https://github.com/Klipper3d/klipper`

## Process focus
- Ambient-temperature dual-mass extrusion (no heated bed, no thermal extrusion loop).
- Optional flow sensor feedback.
- Optional IO-Link integration through an external bridge.
- Servo-controlled alginate valve for synchronized co-deposition.

## Platform requirements
- Operator workstation compatibility: Windows 10 and Windows 11.
- Klipper host runtime: Linux environment (CB1/CM4 class).
- Secure internet connectivity for remote management and updates.
- Integrated process camera for remote supervision.

## Quick start
1. Complete final part numbers in `docs/BOM.md`.
2. Replace placeholders in `config/klipper/printer.cfg` with real pins and values.
3. Configure camera service from `config/camera/crowsnest.conf.example`.
4. Wire panel buttons and map signals from `config/electrical/panel_io_map.csv`.
5. Integrate non-safety panel inputs using `config/klipper/panel_inputs.cfg.example`.
6. Test safety chain and button behavior with dry runs.
7. Pin a validated Klipper commit hash after commissioning.

