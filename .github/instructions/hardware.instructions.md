# Hardware Instructions

## Hardware in this project
- Seeed Studio XIAO ESP32-C3
- Grove Base for XIAO
- SGP41 air quality sensor
- LIS3DH accelerometer
- AHT20 + BMP280 environmental sensor
- SSD1315 / SSD1306-compatible 0.96" I2C OLED
- MP1584EN buck converter (12V -> 5V)
- Optional IRLB8721 MOSFET for future fan control

## Wiring assumptions
- Primary input power is 12V, reduced to 5V using MP1584EN.
- ESP32 board is powered from 5V.
- I2C devices are powered from 3.3V unless a specific breakout explicitly supports 5V logic and power.
- All I2C devices share one common SDA/SCL bus.
- Ground must be common across the entire system.
- Keep sensor wiring short and neat.

## Documentation rules
- Wiring instructions should include:
  1. a pin mapping table
  2. a bus-level wiring summary
  3. power guidance
  4. notes on soldering and layout practice
- Assembly guidance should be step-by-step.
- Flag ambiguity clearly instead of guessing.

## Future expansion
- Treat IRLB8721 as reserved for optional fan control unless explicitly requested.
- If fan control is added, use safe default OFF behavior on boot.
