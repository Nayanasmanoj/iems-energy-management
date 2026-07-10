# IEMS - IoT Based Energy Management System

An IoT-based system that lets users monitor real-time electricity consumption and remotely control household appliances through a mobile app â€” built to address the problem of high, unexplained electricity bills and appliances left running unattended.

This was built as a team B.Tech Electronic Product Design project at the Division of Electronics Engineering, School of Engineering, CUSAT (April 2025).

## Problem It Solves

In most Indian households, electricity bills arrive once every two months, giving no visibility into daily usage until it's too late. People also frequently worry about appliances (irons, motors, etc.) being left on after they've left home. IEMS addresses both problems with real-time monitoring, remote control, and threshold-based alerts.

## Features

- **Real-time energy monitoring**  live voltage, current, and power readings
- **Remote appliance control**  turn devices on/off from anywhere via a mobile app
- **Consumption threshold alerts**  set a target bill/usage limit and get notified when exceeded
- **Emergency turn-off**  instantly cut power to a connected appliance
- **Load classification**  separate light-load and heavy-load control per room
- **Cloud-based data logging** historical usage trends via Firebase

## Hardware

| Component | Purpose |
|---|---|
| ESP32 WROOM-32 | Central microcontroller  Wi-Fi, data processing, control logic |
| ZMPT101B | AC voltage sensing (isolated, analog output) |
| ACS712 | AC current sensing (Hall-effect based) |
| Single-channel relay module | Switches appliance load ON/OFF |
| AC-DC power supply module (220V â†’ 5V) | Powers the ESP32 and sensor modules |

**Pin mapping (ESP32):**
- GPIO32 Relay IN
- GPIO34 ACS712 analog output (current)
- GPIO35 ZMPT101B analog output (voltage)

## Software / Architecture

- **Firmware:** Arduino IDE (C/C++) on ESP32 reads sensors, computes power/energy, hosts a local web server, and drives the relay
- **Backend:** Firebase (Realtime Database, Authentication, Cloud Functions, Firebase Cloud Messaging) for data storage, auth, and push alerts
- **Mobile App:** React Native (cross-platform)  live dashboard, remote control panel, notifications, budget/threshold settings

### Data Flow
```
Power Supply Voltage/Current Sensing (ZMPT101B, ACS712)
            ESP32 reads & computes power/energy
            Threshold check
             Data pushed to Cloud (Firebase)
            Mobile App displays data / sends control commands
            ESP32 activates/deactivates relay
```

## Results (from testing)

- Voltage readings accurate within ±2V, current within ±0.2A vs. reference multimeter
- Relay response time from mobile command to physical switching: **under 1 second**
- Ran continuously for 72+ hours with stable Wi-Fi/cloud connectivity and no component failure
- Passed functionality, usability, reliability, performance, and safety testing (isolation, overload handling, short-circuit protection)

## Total Hardware Cost

‚¹1,524 (ESP32, sensors, relay, power supply, connectors, enclosure)

## Firmware Snippet

The ESP32 firmware reads current/voltage, computes power and cumulative energy (kWh), persists the running total to EEPROM, and serves a lightweight local web page with a relay toggle button. Full firmware is in `/firmware`.

## My Role

I worked on this as part of a 5-member team, contributing to sensor integration (ZMPT101B/ACS712 wiring and calibration) and system testing/validation.

## Future Scope

- AI-based predictive energy analytics
- Battery backup for outage resilience
- Integration with solar/renewable sources
- Support for LoRa/GSM for off-grid or rural deployments

## Team

Rio Roy · Varghese Selestin · Athul K S · Mohammed Shan · Nayana S M
