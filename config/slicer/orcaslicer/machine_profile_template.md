# Helix OrcaSlicer Machine Template (Draft)

Machine name: Helix-Cartesian-500

## Geometry
- Bed shape: Rectangular
- Bed size X: 500 mm
- Bed size Y: 500 mm
- Max Z: <TBD>
- Origin: Front-left

## Kinematics
- Type: Cartesian
- Number of print heads: 2

## Process model
- Ambient-temperature material deposition
- No heated bed
- Custom feeder and valve synchronization (macro-dependent)

## Firmware/communication
- Firmware: Klipper
- Upload method: Moonraker API

## G-code placeholders
- Start G-code: pending (must call Helix macros)
- End G-code: pending
- Toolchange G-code: pending

## Calibration prerequisites before final profile
1. Axis steps/rotation_distance verified.
2. Feeder A/B flow characterization complete.
3. Alginato valve timing map complete.
4. Safe travel and retraction strategy validated.
