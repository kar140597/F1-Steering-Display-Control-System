# F1-Steering-Display-Control-System
Developing Steering Display Control System for F1 is part of my Electronics System Design project. The goal of project emphasized in developing system with strict budget of €100, the group was divided into project management, Hardware, Firmware and GUI development. I personally took care of firmware part. This is project is a success in all counts. Report and code attached for reference.
## Overview
This project implements a custom **Steering Wheel Display Electronic Control Unit (ECU)**
for Formula1.  
The ECU manages driver inputs (buttons, clutch paddle, rotary encoders),
communicates vehicle data over **CAN bus**, and displays real-time telemetry
on a **TFT display**.

The system was designed with automotive constraints in mind, including
robust power management, deterministic firmware behavior, and modular
hardware–software integration.

---

## System Architecture
- **Input Layer**
  - Push buttons (gear up/down, DRS mode selection, Ignition)
  - Analog clutch paddle (ADC-based)
  - Rotary encoder (menu / parameter selection)

- **Processing Layer**
  - STM32 microcontroller
  - Real-time input processing
  - State-based logic for gear, clutch, ignition, and DRS control

- **Communication Layer**
  - CAN bus (vehicle network interface)
  - Periodic transmission of steering wheel status frames
  - Receive Temperature Data and provide error accordingly

- **Output Layer**
  - TFT display (ILI9341)
  - Real-time visualization of:
    - Gear position
    - Clutch percentage
    - Engine / battery temperature
    - System status flags

---

## Hardware Components
- **Microcontroller**: STM32 (F1 / F4 / G4 family)
- **Display**: ILI9341 TFT (SPI)
- **CAN Transceiver**: SN65HVD23x (automotive-grade)
- **Sensors & Inputs**:
  - Analog clutch potentiometer
  - Digital buttons
  - Rotary encoder
- **Power Management**:
  - Ignition-controlled display enable (DSP_EN)
  - Decoupling capacitors and EMI protection

---

## Firmware Features
- HAL-based STM32 firmware
- Deterministic main loop with non-blocking updates
- ADC filtering for clutch input
- CAN message framing and transmission
- TFT graphics rendering with custom UI layout
- Safe display power cycling via ignition logic

---

## Software Structure
Core/
├── Src/
│ ├── main.c
│ ├── can.c
│ ├── adc.c
│ ├── gpio.c
│ └── ui_display.c
├── Inc/
Drivers/
ILI9341/

## CAN Communication
- Periodic transmission of steering wheel state
- Example signals:
  - Gear number
  - Clutch percentage
  - Button states
  - DRS enable status
  - Engine Temperature
  - Tire Temperature
CAN baud rate (500 kbps) and message IDs are configurable in firmware.

---

## Display UI
- Static layout with dynamic data fields
- Flicker-free partial updates
- Ignition-based power sequencing to ensure correct initialization

---

## How to Build & Flash
1. Open the project in **STM32CubeIDE**
2. Select the correct target MCU
3. Build the project
4. Flash via **ST-Link**
5. Power the ECU and toggle ignition input

---

## Results
- Reliable CAN transmission under continuous operation
- Stable TFT display behavior across power cycles
- Responsive clutch and button input handling
- Modular code structure suitable for extension

---

## Future Improvements
- RTOS-based task scheduling
- CAN reception and diagnostics
- EEPROM-based configuration storage
- Automotive watchdog integration
- IP-rated enclosure and EMC testing

---

## Author
**Kartik Kanchan**  
MSc Electronic Engineering for Intelligent Vehicles (Electronic and Communication System)  
MUNER
