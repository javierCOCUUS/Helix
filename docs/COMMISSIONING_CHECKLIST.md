# Helix - Commissioning Checklist (Cartesian, Ambient Dual-Mass)

Date: 2026-03-12
Machine baseline: Cartesian architecture, 500x500 mm printable area, ambient-temperature dual-mass extrusion.

## 1) Pre-Assembly
- [ ] Confirm final architecture lock: Cartesian (not CoreXY).
- [ ] Freeze BOM revision and purchasing list.
- [ ] Confirm panel layout drawing and cable routing plan.
- [ ] Confirm safety component ratings (contactor, safety relay, breakers).
- [ ] Confirm host strategy (CB1/CM4 or industrial mini PC).

## 2) Mechanical Build
- [ ] Assemble base frame and check diagonals (max mismatch target: <= 1.0 mm).
- [ ] Install vertical columns and top frame; verify squareness.
- [ ] Install XY rails and verify smooth full travel without binding.
- [ ] Install Z structure and bed/platform support.
- [ ] Install dual material feeders and hopper/mechanical supports.
- [ ] Install alginate valve mechanism and servo linkage.

## 3) Electrical Panel Build
- [ ] Install main disconnect, branch protection, safety relay, contactor.
- [ ] Wire E-Stop and guard chain as hardwired safety loop.
- [ ] Install 24V PSU (logic) and 48-80V PSU (driver power).
- [ ] Tie DC negatives for shared signal reference (24V V- and HV PSU V-).
- [ ] Wire DM860T signal inputs from controller (PUL/DIR/ENA).
- [ ] Wire panel pushbuttons and indicators per IO map.
- [ ] Validate PE grounding continuity.

Reference files:
- `docs/ELECTRICAL_PANEL_AND_SAFETY.md`
- `config/electrical/panel_io_map.csv`

## 4) Controller and Software
- [ ] Install Klipper host stack (Linux): Klipper + Moonraker + Mainsail/Fluidd.
- [ ] Flash/prepare board and connect MCU serial.
- [ ] Populate `config/klipper/printer.cfg` placeholders.
- [ ] Include panel inputs file if used (`panel_inputs.cfg.example`).
- [ ] Configure camera service from `config/camera/crowsnest.conf.example`.
- [ ] Validate Windows 10/11 operator station access via browser.

## 5) Motion and Feeder Bring-Up (Dry)
- [ ] Jog X/Y/Z and verify axis direction.
- [ ] Verify limits/endstops.
- [ ] Jog feeder A/B at low speed and confirm direction.
- [ ] Confirm ENA behavior: motors release when disabled.
- [ ] Validate alginate valve open/close angles without mechanical stress.

## 6) Safety Functional Test (FAT)
- [ ] E-Stop drops hazardous power immediately.
- [ ] No automatic restart after safety reset.
- [ ] Door/interlock event triggers expected safe state.
- [ ] Local/Remote selector gates remote commands correctly.
- [ ] Stop/Pause buttons trigger expected software behavior.
- [ ] Alarm indicators (H3/H5) function as expected.

## 7) Process Validation
- [ ] Prime feeder A and feeder B independently.
- [ ] Measure real flow vs commanded movement and tune rotation distance.
- [ ] Run co-deposition test (A + alginate valve).
- [ ] Run long-duration stability test (>= 2 hours).
- [ ] Validate clean shutdown and restart procedure.

## 8) Remote Operations Validation
- [ ] Verify outbound internet connectivity.
- [ ] Verify VPN remote access (no public direct ports).
- [ ] Verify camera stream latency and reliability.
- [ ] Verify remote update procedure + rollback notes.
- [ ] Backup `printer.cfg`, macros, and panel settings.

## 9) Handover Package
- [ ] Final as-built wiring diagram.
- [ ] Final IO mapping table.
- [ ] Final pinned firmware commits (submodules).
- [ ] Maintenance SOP (daily/weekly/monthly).
- [ ] Operator quick guide (Windows 10/11).
