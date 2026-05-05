# Wiring Guide

This document defines the baseline wiring for the UV printer monitor build.

## 1) Pin mapping table

| Function | Device | ESP32-C3 (XIAO) Pin | Notes |
|---|---|---|---|
| I2C SDA | Shared I2C bus | GPIO6 | Confirm against your exact XIAO ESP32-C3 board revision |
| I2C SCL | Shared I2C bus | GPIO7 | Confirm against your exact XIAO ESP32-C3 board revision |
| 3.3V power | I2C sensors + OLED | 3V3 | Preferred for logic safety |
| 5V power | XIAO board input | 5V | From MP1584EN buck converter |
| Ground | All modules | GND | Common ground across all modules |

## 2) Bus-level wiring summary

- Use one shared I2C bus for SGP41, LIS3DH, AHT20, BMP280, and OLED.
- Connect every module SDA to SDA and every module SCL to SCL.
- Keep total bus wiring short and avoid unnecessary branch stubs.
- If instability appears, reduce wire length first before changing pull-up strategy.

## 3) Power guidance

- Input power: 12V DC.
- Convert 12V to 5V using MP1584EN, then feed 5V to the XIAO board.
- Use 3.3V rail for I2C sensors and OLED unless a module explicitly requires 5V and supports logic translation.
- Verify buck converter output with a multimeter before connecting the ESP32.
- Ensure all grounds are tied together.

## 4) Soldering and layout notes

- Tin wires and pads before final soldering to reduce heating time on boards.
- Add strain relief where cables leave the enclosure.
- Route power wiring separately from signal wiring when possible.
- Label wires or use color coding for faster troubleshooting.
- Secure modules to reduce vibration-induced connector issues.

## Assembly steps

1. Set MP1584EN output to a stable 5V with no load connected.
2. Connect 5V and GND from buck converter to XIAO power pins.
3. Build the shared I2C bus from XIAO to all I2C modules.
4. Connect 3.3V and GND to each I2C module.
5. Power on and run I2C scan in ESPHome logs.
6. Confirm all sensors and OLED are detected before final enclosure assembly.

## Ambiguities to validate

- Confirm the exact SDA/SCL pins used by your physical XIAO ESP32-C3 board revision.
- Confirm each breakout board voltage and logic-level requirements before permanent wiring.
