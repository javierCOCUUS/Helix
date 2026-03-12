# Helix - Flow Sensor and IO-Link Integration Notes

## Scope
This document defines practical options to add real process feedback to a cold dual-mass extrusion machine in Klipper.

## 1) Can Klipper use flow sensors directly?
Yes, if the sensor output is electrically simple:
- Pulse output (PNP/NPN, encoder-like): map to a digital input pin and count events.
- Analog output (0-10V or 4-20mA): requires signal conditioning and an ADC path compatible with your controller.

For first bring-up, pulse-output sensors are the fastest path.

## 2) IO-Link compatibility
IO-Link is not natively supported by Klipper.

You can still use IO-Link by adding an external bridge:
1. IO-Link sensor/actuator -> IO-Link Master
2. IO-Link Master -> PLC/IPC/Service layer
3. Bridge -> Klipper action via macros, digital I/O, or API calls

Recommended approach:
- Start with direct wired sensors for machine commissioning.
- Add IO-Link later when process KPIs and alarms are stable.

## 3) Alginato valve with servo (supported)
A servo valve is straightforward in Klipper using `[servo]` and macros.

Typical control flow:
1. Open valve (`ALGINATE_ON`)
2. Extrude material A for a defined segment
3. Close valve (`ALGINATE_OFF`)

This is already reflected in `config/klipper/printer.cfg` macros.

## 4) Reliability recommendations
- Use a dedicated 5V rail for the servo (shared ground with controller).
- Add mechanical end-stops or hard limits in the valve linkage.
- If available, add pressure sensor alarms to stop extrusion when over-pressure is detected.
- Log feeder steps vs measured flow to detect slip or blockage.

## 5) Open engineering items
- Final sensor model and output interface (pulse, analog, IO-Link).
- Sampling rate and alarm thresholds.
- Whether alginate dosing is event-based or continuously proportional.
- Whether closed-loop compensation is required in real time.
