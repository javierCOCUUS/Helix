# OrcaSlicer Profile Placeholder

This folder is reserved for future OrcaSlicer machine/process profiles.

## Why placeholder only (for now)
Helix uses ambient dual-mass extrusion with custom feeders and valve logic.
A production slicer profile should be created only after:
- motion calibration,
- feeder calibration,
- valve timing calibration,
- process test prints.

## Planned files
- `machine_profile_template.md`
- `process_profile_template.md`
- `start_end_gcode_template.gcode`

## Notes
- OrcaSlicer profile export/import format can evolve between versions.
- Keep this folder versioned in repo, then store final exported profile files here when ready.
