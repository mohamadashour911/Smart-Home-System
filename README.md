# Smart Switch V2.0 - Semi-Industrial Smart Workshop

Welcome to the official repository of Smart Switch V2.0, an advanced automation and telemetry platform designed for semi-industrial smart workshop environments. This system enables intelligent high-power switching, live power monitoring, and low-latency mesh communication.

---

## Project Overview
* **The Problem:** Traditional workshops and industrial environments suffer from high energy waste due to unmonitored idle machinery, safety hazards from unmanaged high-voltage switching, and a lack of real-time power consumption data. Manual operation of heavy-duty loads often leads to electrical arcing and system failures.
* **The Solution:** This project delivers a Semi-Industrial Smart Workshop automation system. It introduces centralized, intelligent control for heavy electrical loads (up to 16A), integrating precise current sensing, robust arc suppression, and fail-safe communication to isolate the user from dangerous high-voltage lines while collecting live telemetry.

---

## Hardware Components
* **Microcontroller (MCU):** ESP32-WROOM-32 – Selected for its high-speed processing, built-in ADC for telemetry, and dual Wi-Fi/Bluetooth capabilities.
* **Power Supply Module:** HLK-PM01 (5V) – An ultra-compact, isolated step-down power supply module used to step down the 220V AC mains to a stable 5V DC rail.
* **Voltage Regulator:** AMS1117-3.3 – Drops the 5V rail down to an accurate 3.3V DC to power the ESP32 and digital sensors safely.
* **High-Power Switching:** FH17-1A2TLE-DC5V Subminiature Power Relays – Heavy-duty, sensitive-coil 5V relays capable of switching inductive and resistive industrial loads up to 16A.
* **Switching Actuators:** MMBT3904LT1G NPN Transistors – Configured as Low-Side switches to safely drive the 5V relay coils from the ESP32 GPIOs.
* **Current Sensing & Telemetry:** ACS712ELCTR-20A – A fully isolated Hall-effect based linear current sensor used to monitor live load currents.
* **Arc Suppression & Protection:**
  * **RC Snubber Circuit (56 Ohm / 2W Resistor + 4.7nF Capacitor):** Placed in series across the relay contacts to suppress inductive voltage spikes and eliminate contact welding during AC high-current switching.
  * **Varistor (MOV):** Connected across the AC mains entry to clip high-voltage transient surges and protect the entire board.
* **Signal Conditioning (Hardware Filtering):**
  * **4.7nF Filter Capacitors:** Hooked directly to Pin 6 (FILTER) of the ACS712 sensors to lower the noise bandwidth down to 20kHz.
  * **Voltage Divider (56kOhm / 100kOhm):** Steps down the 5V maximum sensor output down to a linear 2.88V, perfectly matching the ESP32 ADC limits.

---

## Protocols
* **ESP-NOW Protocol:** A low-power, connectionless wireless communication protocol developed by Espressif. It is utilized here to achieve instant, peer-to-peer data transmission between the workshop nodes and the central gateway with near-zero latency, completely bypassing the need for a local Wi-Fi router.

---

## Visuals and Design

### System Schematic
Here is the full system schematic showing the isolation barriers between the low-voltage MCU side and the high-voltage 220V AC rails:
<img width="942" height="682" alt="image" src="https://github.com/user-attachments/assets/bbfe896b-4486-4e6e-b204-cae0bd9ac2c6" />


### 3D PCB Layout - Top View
Showcases the compact arrangement of the HLK-PM01, the dual power relays, and the clean routing of the communication lines:
<img width="643" height="503" alt="2" src="https://github.com/user-attachments/assets/99cafa27-6dc6-42c8-8476-a121d1f63c8b" />


### 3D PCB Layout - Bottom View
Highlights the massive high-current copper polygons, the custom 2mm clearance gaps, the isolation slots cut into the PCB substrate for arc avoidance, and the exposed solder mask paths designed for physical tin reinforcement:
<img width="757" height="562" alt="1" src="https://github.com/user-attachments/assets/3d748d87-1cb8-4a36-9b9e-e127b64f1a1f" />

