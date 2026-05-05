# ESPHome Instructions

## Defaults
- Default to ESPHome YAML unless explicitly asked for Arduino or ESP-IDF/C++ code.
- Prefer simple, robust configurations over clever or highly abstract solutions.
- Keep configuration readable and heavily commented.
- Preserve compatibility with Home Assistant entities and naming conventions.
- Use clear IDs for sensors and binary sensors.
- When generating YAML, avoid duplicate IDs and invalid indentation.
- Prefer maintainability over micro-optimizations.

## Sensor behavior
- SGP41 should use humidity and temperature compensation.
- SGP41 values are trend indicators, not lab-grade absolute measurements.
- LIS3DH should detect printer activity from vibration over time, not single impacts.
- Printer activity detection should use smoothing, delayed_on, and delayed_off to reduce false triggers.

## Firmware entities
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
- Avoid noisy high-frequency updates unless explicitly requested.
- Prefer template sensors for derived values such as vibration magnitude.

## Display behavior
- Keep OLED layout simple and readable.
- Show only key live values:
  - printer active / idle
  - VOC index
  - temperature
  - humidity
- Avoid display clutter unless extra pages are explicitly requested.

## Pin and bus policy
- Do not invent hardware pins if not specified.
- Use the XIAO ESP32-C3 I2C pins defined by the project.
- All I2C devices share the same SDA and SCL bus.
