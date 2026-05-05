# enclosuresensor

DIY ESP32-based UV printer workspace monitor using ESPHome and Home Assistant.

## Features

- Printer activity detection with LIS3DH vibration sensing
- VOC and NOx trend monitoring with SGP41
- Temperature, humidity, and pressure reporting
- Local live status on a 0.96 inch I2C OLED
- Home Assistant integration through ESPHome

## Project layout

- `.github/` Copilot instructions for firmware and hardware work
- `firmware/uv_air_monitor.yaml` main ESPHome configuration
- `docs/wiring.md` wiring and power guidance
- `docs/bom.md` bill of materials

## First boot

1. Copy `secrets.example.yaml` to `secrets.yaml` and fill in your Wi-Fi credentials.
2. Verify the buck converter output is a stable 5V before connecting the XIAO ESP32-C3.
3. Confirm SDA and SCL match your exact XIAO ESP32-C3 board revision.
4. Flash `firmware/uv_air_monitor.yaml` with ESPHome.
5. Check the ESPHome logs and confirm all expected I2C devices are detected.
6. Verify temperature, humidity, pressure, VOC, NOx, and acceleration entities appear in Home Assistant.
7. Confirm the OLED displays printer state, VOC, temperature, and humidity.

## Activity calibration

The initial vibration settings are intentionally conservative.

1. Let the printer sit idle for several minutes and note the `vibration_level` range.
2. Start a representative print and note the sustained `vibration_level` range during normal operation.
3. Set `vibration_active_threshold` in `firmware/uv_air_monitor.yaml` slightly above idle and below the sustained running range.
4. Increase `vibration_delayed_on` if bumps or handling trigger false starts.
5. Increase `vibration_delayed_off` if short pauses during printing cause false idle transitions.
6. Increase `vibration_window_size` if the signal is too noisy; reduce it if state changes feel too slow.

## Future improvement option

The current firmware uses raw acceleration magnitude because it is simple and easy to tune.

There is also a documented delta-from-1g option in `firmware/uv_air_monitor.yaml` for future refinement. That approach removes most of the static gravity component and can improve robustness when mounting angle changes or when raw magnitude thresholds are hard to separate.
