# Helix - Remote Connectivity and Camera Architecture

## 1) Target Capability
Helix shall support:
- Secure internet connectivity for remote support.
- Remote operation/monitoring interface for authorized users.
- Live process camera stream for supervision and traceability.

## 2) Recommended Topology
1. Machine LAN segment (industrial VLAN or dedicated subnet).
2. Klipper host (CB1/CM4) connected via Ethernet (preferred) or managed Wi-Fi.
3. Router/firewall with outbound-only policy by default.
4. Remote access through VPN (preferred) instead of direct port forwarding.

## 3) Remote Access Options
- Preferred: Site-to-site or client VPN (WireGuard/OpenVPN class setup).
- Acceptable: Reverse tunnel solution with MFA and audit logs.
- Avoid in production: Publicly exposed web ports without VPN.

## 4) Camera Stack
- Camera service: Crowsnest or equivalent webcam streamer on the Klipper host.
- UI integration: Mainsail/Fluidd webcam panel.
- Baseline recommendation:
  - Resolution: 1280x720 or 1920x1080
  - Frame rate: 15-30 FPS
  - Fixed focus and stable lighting
- Optional second camera for hopper/nozzle close-up.

## 5) Security Requirements
- Unique credentials per machine.
- MFA for all remote admin access.
- OS and package update policy with maintenance windows.
- Access logging for remote sessions and configuration changes.
- Camera stream access restricted to authenticated users.

## 6) Operations Requirements
- Support remote firmware/config updates with rollback plan.
- Define backup cadence for `printer.cfg`, macros, and service configs.
- Keep an offline recovery image for host storage replacement.

## 7) Windows 10/11 Operator Experience
- Operators use Windows 10/11 workstations to access the machine UI via browser.
- Recommended browsers: latest Chromium-based or Firefox ESR.
- If needed, provide remote desktop jump host for support staff.

## 8) Commissioning Checklist (Remote)
1. Verify LAN connectivity and DNS/NTP sync.
2. Enable VPN and test remote login from external network.
3. Validate webcam stream in Mainsail/Fluidd.
4. Perform controlled remote update and rollback test.
5. Document credentials handover and emergency contacts.
