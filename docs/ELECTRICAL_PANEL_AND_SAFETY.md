# Helix - Electrical Panel and Safety Concept (Draft v0.1)

## Scope
Functional electrical-panel concept for Helix with safety chain and operator pushbuttons.

Important: This is an engineering draft for design alignment. Final execution must be reviewed and signed by a qualified electrical engineer according to local regulations.

## 1) Main Architecture
- Incoming supply: `3x400V AC + PE` (as per quotation baseline).
- Main disconnect switch (`QS1`) on door.
- Branch protection (`QF*` MCB/fuses) for each load group.
- Safety chain controls a main contactor (`KM1`) via safety relay (`SR1`).
- Separate DC supplies:
  - `PS1` 24VDC control/logic.
  - `PS2` 48-80VDC (target 60VDC) for DM860T drivers.
- Common DC reference between PS1 and PS2 negatives (signal integrity requirement).

## 2) Safety Chain (Hardwired)
Recommended hardwired sequence:
1. `S0` Emergency Stop (NC, dual-channel) -> `SR1` safety relay inputs.
2. Guard-door interlock(s) (NC, dual-channel where applicable) -> `SR1`.
3. `SR1` safety outputs drive `KM1` contactor coil.
4. `KM1` removes power from motion/actuation branches when safety is open.
5. Manual reset pushbutton (`S2`, NO) required after safety event.

This chain should not depend on software to remove hazardous motion power.

## 3) Recommended Pushbuttons and Switches
- `S0` E-Stop (red mushroom, latching, NC, dual-channel).
- `S1` Stop pushbutton (black, NC) for controlled process stop.
- `S2` Safety reset (blue, NO).
- `S3` Start cycle (green, NO).
- `S4` Pause/hold (yellow, NO).
- `S5` Homing enable (white, NO) optional.
- `SA1` Local/Remote selector (2-position key switch).
- `SA2` Maintenance enable key switch (optional but recommended).

## 4) Indicators
- `H1` Main power ON (white).
- `H2` Control power 24V OK (green).
- `H3` Safety chain open/fault (red).
- `H4` Remote session active (blue).
- `H5` Alarm/warning (amber).

## 5) Functional Single-Line (Text)
```text
3x400VAC -> QS1 -> QF_MAIN -> SR1/KM1 safety-controlled bus
                                 |-> QF_PS1 -> PS1 24VDC -> Manta + I/O + fans + signals
                                 |-> QF_PS2 -> PS2 60VDC -> DM860T #1/#2 power
                                 |-> QF_AUX -> auxiliaries (lights, IPC/router, camera PSU)

S0(E-STOP NC chA/chB) + door interlocks -> SR1 -> KM1 coil
S2(RESET NO) -> SR1 reset input
```

## 6) Controller Integration Concept
- Safety critical stop: hardwired by `SR1/KM1`.
- Software stop/pause: buttons read by controller digital inputs.
- E-Stop status mirrored to controller input for diagnostics only.
- Remote mode (`SA1`) gates whether remote commands are accepted.

## 7) Network and Remote Support Loads in Panel
- Industrial router/firewall on protected auxiliary branch.
- Managed switch (optional) for camera + host segregation.
- UPS or DC hold-up (optional) for graceful shutdown of compute host.

## 8) Verification Checklist (Panel FAT)
1. Verify E-Stop immediately drops hazardous motion power.
2. Verify no auto-restart after safety reset.
3. Verify Local/Remote selector behavior.
4. Verify Start/Pause/Stop mapping in software.
5. Verify contactor dropout time and brake behavior.
6. Verify PE continuity and insulation tests.

## 9) Open Engineering Items
- Final protective device ratings (short-circuit and cable sizing).
- PL target (ISO 13849) and architecture category selection.
- Exact interlock type for guards/access panels.
- Need for STO-capable servo/drive path if future axes are servo-based.
