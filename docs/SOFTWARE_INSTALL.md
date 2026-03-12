# Helix - Software Installation Guide

Date: 2026-03-12
Target: Manta M8P + Raspberry Pi CM4 host (Linux) + Windows 10/11 operator workstation.

## 1) Scope
This guide covers software stack installation for:
- Klipper host runtime (Linux)
- Moonraker API
- Mainsail/Fluidd UI
- Camera service (Crowsnest)

## 2) Host OS Preparation (CM4)
1. Flash a Linux image compatible with CM4 (Raspberry Pi OS Lite recommended).
2. Enable SSH and set static/reserved IP on your machine network.
3. Update system packages:
```bash
sudo apt update && sudo apt full-upgrade -y
sudo reboot
```

## 3) Install Klipper Stack (recommended: KIAUH)
1. Login to host over SSH.
2. Install prerequisites:
```bash
sudo apt install -y git
```
3. Clone and run KIAUH:
```bash
git clone https://github.com/dw-0/kiauh.git
cd kiauh
./kiauh.sh
```
4. In KIAUH, install:
- Klipper
- Moonraker
- Mainsail (or Fluidd)
- Crowsnest (if camera is required)

## 4) Board Firmware Build/Flash
1. Use linked repositories in this project:
- `external/klipper`
- `external/manta-m8p`
2. Build MCU firmware for Manta M8P variant in use.
3. Flash according to BTT Manta M8P procedure.
4. Confirm MCU serial path is visible on host:
```bash
ls /dev/serial/by-id/
```

## 5) Deploy Helix Configuration
1. Copy baseline configs from this repo to your Klipper config directory.
- Main: `config/klipper/printer.cfg`
- Optional panel inputs: `config/klipper/panel_inputs.cfg.example`
- Optional camera template: `config/camera/crowsnest.conf.example`
2. Replace all placeholders (`<...>`) with real pin/value data.
3. Restart services and verify no config parse errors.

## 6) Windows 10/11 Operator Setup
1. Use a modern browser (Edge/Chrome/Firefox).
2. Open Mainsail/Fluidd at host IP address.
3. Add bookmarks for:
- Main UI
- Camera stream URL
4. Validate basic actions:
- Connect/reconnect
- Upload gcode
- Start/pause/stop

## 7) Camera Setup
1. Install/configure Crowsnest.
2. Start with one camera (`/dev/video0`, 1280x720, 20 FPS).
3. Verify stream inside UI and tune FPS/resolution if needed.

## 8) Remote Access Setup (Recommended)
1. Configure VPN or secure tunnel (no direct public ports).
2. Test remote access from external network.
3. Validate remote update workflow and rollback notes.

## 9) Acceptance Checks
- Klipper services start on boot.
- MCU connects reliably.
- UI accessible from Windows 10 and Windows 11.
- Camera visible in UI.
- Backup of final config completed.

## 10) Maintenance
- Pin and record tested commit hashes after commissioning.
- Backup config before any update.
- Update in maintenance windows only.
