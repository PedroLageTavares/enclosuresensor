# GitHub Copilot Instructions

## Project overview
This project is a DIY ESP32-based monitoring device for a UV printer workspace.
Main goals:
- Detect printer activity using a LIS3DH accelerometer.
- Monitor air quality using an SGP41 VOC/NOx sensor.
- Monitor temperature and humidity for gas compensation.
- Show local status on a 0.96" I2C OLED display.
- Integrate with Home Assistant using ESPHome.
- Keep the design simple, reliable, and easy to maintain.

## Hardware in this project
- Seeed Studio XIAO ESP32-C3
- Grove Base for XIAO
- SGP41 air quality sensor
- LIS3DH accelerometer
- AHT20 + BMP280 environmental sensor
- SSD1315 / SSD1306-compatible 0.96" I2C OLED
- MP1584EN buck converter (12V -> 5V)
- Optional IRLB8721 MOSFET for future fan control

## General coding rules
- Default to ESPHome YAML unless explicitly asked for Arduino or ESP-IDF/C++ code.
- Prefer simple, robust configurations over clever or highly abstract solutions.
- When proposing automations, use conservative thresholds and explain which values should be tuned experimentally.
- Do not invent hardware pins if not specified; use the XIAO ESP32-C3 I2C pins defined by the project.
- Keep configuration readable and heavily commented.
- Preserve compatibility with Home Assistant entities and naming conventions.
- Use clear IDs for sensors and binary sensors.
- When generating YAML, avoid duplicate IDs and invalid indentation.
- Prefer maintainability over micro-optimizations.

## Sensor-specific behavior
- SGP41 should use humidity and temperature compensation.
- SGP41 values are best treated as trend indicators, not lab-grade absolute measurements.
- LIS3DH should be used to detect machine activity by measuring vibration/movement over time, not single impact events.
- Printer activity detection should use smoothing, delayed on, and delayed off logic to avoid false triggers.

## Preferred firmware behavior
- Expose entities for:
  - temperature
  - humidity
  - pressure
  - VOC index
  - NOx index
  - acceleration x/y/z
  - vibration level
  - printer active state
- Use stable update intervals suitable for Home Assistant dashboards.
- Avoid very noisy high-frequency updates unless explicitly requested.
- Prefer template sensors for derived values such as vibration magnitude.

## Display behavior
- Keep OLED layout simple and readable.
- Show only key live values:
  - printer active / idle
  - VOC index
  - temperature
  - humidity
- Avoid cluttering the display with too many pages unless explicitly requested.

## Documentation rules
- When generating wiring instructions, provide:
  1. a pin mapping table
  2. a bus-level wiring summary
  3. power guidance
  4. notes on good soldering and layout practice
- When generating assembly guidance, prefer step-by-step instructions.
- Flag any ambiguity clearly instead of guessing.

## Future expansion
- The IRLB8721 should be treated as reserved for optional fan control unless explicitly requested.
- If fan control is added, propose safe default off behavior on boot.

## Additional instruction files
- See .github/instructions/esphome.instructions.md for firmware and entity conventions.
- See .github/instructions/hardware.instructions.md for wiring, power, and assembly conventions.
