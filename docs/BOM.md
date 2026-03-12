# Helix - Bill of Materials (BOM)

## 1) Control and Compute
| Item | Qty | Recommended Model | Specs / Notes | Status |
|---|---:|---|---|---|
| Main controller | 1 | BTT Manta M8P V2.0 | 24V logic power, onboard driver slots, CB1/CM4 compatible | Selected |
| Compute module | 1 | BTT CB1 (or Raspberry Pi CM4) | Runs Klipper host + Moonraker + Mainsail/Fluidd | Pending final |
| Storage | 1 | eMMC / microSD | OS + config backup strategy | Pending |

## 2) Motion Drivers and Motors
| Item | Qty | Recommended Model | Specs / Notes | Status |
|---|---:|---|---|---|
| External material drivers | 2 | StepperOnline DM860T | 24-80VDC input, opto-isolated STEP/DIR/ENA for screw feeders | Selected |
| Axis drivers (X/Y/Z) | 3 to 5 | TMC5160 | For high-current motion axes on Manta slots | Selected |
| Material motors | 2 | NEMA 23/34 (worm feeder) | Match torque with hopper pressure and screw load | Pending size |
| X/Y/Z motors | 3+ | NEMA 23 | Size per gantry mass and target acceleration | Pending size |

## 3) Power System
| Item | Qty | Recommended Model | Specs / Notes | Status |
|---|---:|---|---|---|
| PSU A (logic) | 1 | 24V DC PSU | Powers Manta, fans, servos, low-voltage loads | Selected |
| PSU B (torque) | 1 | 48-80V DC PSU (target 60V) | Dedicated supply for both DM860T | Selected |
| AC input protection | 1 set | MCB + fuse + EMI filter | Size by regional code and total current | Pending electrical design |
| Emergency Stop | 1 | Latching NC E-Stop | Cuts AC feed before PSU stage | Selected |
| Main contactor (recommended) | 1 | Coil-rated contactor | Hard power isolation via E-Stop chain | Recommended |

## 4) Ambient Material Delivery (No Thermal Loop)
| Item | Qty | Recommended Model | Specs / Notes | Status |
|---|---:|---|---|---|
| Cold extrusion heads | 2 | Progressive cavity / screw nozzle assembly | Ambient-temperature deposition of two masses | Pending model |
| Back-pressure sensors (optional) | 2 | 0-10V or 4-20mA pressure transducer | Protects against clogging and over-pressure | Recommended |
| Flow sensor (optional) | 1 to 2 | Pulse or analog inline flow sensor | Real material-flow feedback for one or both lines | Recommended |
| Alginato valve | 1 | Servo-actuated pinch/needle valve | Opens during one material stream for co-deposition | Selected concept |
| Valve servo | 1 | 24V->5V powered hobby/industrial servo | Controlled by Klipper `[servo]` output | Pending model |

## 5) Networking, Remote Access, and Camera
| Item | Qty | Recommended Model | Specs / Notes | Status |
|---|---:|---|---|---|
| Industrial router/firewall | 1 | DIN-rail industrial router | VPN-capable secure remote access | Required |
| Managed switch (optional) | 1 | Industrial managed switch | VLAN separation for machine network | Recommended |
| Ethernet cabling | Lot | Cat6 industrial cable | Prefer wired host link over Wi-Fi | Required |
| VPN endpoint | 1 | WireGuard/OpenVPN capable | Encrypted remote maintenance channel | Required |
| Process camera | 1 to 2 | USB/UVC or IP camera | Live monitoring in Mainsail/Fluidd | Required |
| Camera mount and lighting | 1 set | Adjustable mount + LED light | Stable framing of nozzle/part zone | Recommended |

## 6) Machine Safety and I/O
| Item | Qty | Recommended Model | Specs / Notes | Status |
|---|---:|---|---|---|
| Endstops | 3 to 6 | Mechanical/inductive | X/Y/Z limits and homing strategy | Pending final |
| IO-Link master (optional) | 1 | Ethernet IO-Link master | Needed only if using IO-Link sensors/actuators | Optional |
| PLC / protocol bridge (optional) | 1 | Small PLC or IPC | Bridges IO-Link data to Klipper-friendly I/O/macros | Optional |
| Wire and ferrules | Lot | Industrial grade | Ferrules mandatory for screw terminals | Required |
| Grounding kit | Lot | PE star grounding hardware | Chassis + PSU + shields grounding plan | Required |

## 7) Wiring Notes (Critical)
- Tie DC negative of PSU A (24V V-) and PSU B (60V V-) to a common ground reference.
- DM860T logic side:
  - PUL+, DIR+, ENA+ -> +5V logic reference
  - PUL-, DIR-, ENA- -> Manta STEP, DIR, ENABLE outputs
- Route motor power and signal cables separately.
- Use shielded twisted pair for STEP/DIR/ENA lines if cable runs are long.
- E-Stop should de-energize machine power path, not only send firmware signal.
- Servo power should come from a dedicated 5V rail (not directly from MCU signal pin).

## 8) IO-Link Compatibility Note
- Klipper does not natively speak IO-Link.
- IO-Link devices can still be used through an IO-Link master plus a bridge layer (PLC, MQTT/HTTP service, or digital/analog conversion).
- For first machine bring-up, use direct electrical sensors (pulse/analog) before adding IO-Link abstraction.

## 9) Procurement Fields to Complete
- Final voltage/current for PSU A and PSU B
- Exact NEMA frame, current, and holding torque (all motors)
- Screw pitch and gearbox ratio for each feeder
- Flow sensor interface type (pulse, 0-10V, 4-20mA, IO-Link)
- Valve type and servo torque requirement
- Router model, VPN policy, and camera model
- Connector families (aviation, JST, Molex, terminal blocks)

## 10) Bring-up Sequence
1. Bench test Manta + compute only at 24V.
2. Validate X/Y/Z drivers and motion limits without material feed.
3. Wire DM860T logic first, then high-voltage supply.
4. Tune both feeder directions and enable polarity.
5. Validate servo valve macros with dry runs.
6. Add flow sensor feedback and safety interlocks.
7. Validate VPN remote access and camera stream before production.
