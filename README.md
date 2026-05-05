# enclosuresensor

ESP32-C3 enclosure sensor with temperature, humidity, VOC index, and vibration monitoring — configured with [ESPHome](https://esphome.io).

## Features

| Sensor | Chip | Measures |
|---|---|---|
| Temperature & Humidity | SHT31-D | °C, % RH |
| VOC Index | SGP40 | 0–500 VOC index (compensated with SHT31 readings) |
| Vibration / Acceleration | ADXL345 | X/Y/Z acceleration in *g*, composite magnitude, binary vibration alert |

## Hardware

- **Microcontroller** — ESP32-C3-DevKitM-1 (or any ESP32-C3 board)
- **SHT31-D** — temperature & humidity (I2C, address `0x44`)
- **SGP40** — VOC index (I2C, address `0x59`)
- **ADXL345** — 3-axis accelerometer / vibration (I2C, address `0x53`)

All three sensors share the same I2C bus.

## Wiring

| Signal | ESP32-C3 GPIO | All sensors |
|---|---|---|
| SDA | GPIO8 | SDA |
| SCL | GPIO9 | SCL |
| VCC | 3.3 V | VCC |
| GND | GND | GND |

> **ADXL345 address selection**: pull the `SDO/ALT ADDRESS` pin to **GND** for address `0x53` (default) or to **VCC** for `0x1D`.

## Usage

### 1. Clone / download

```bash
git clone https://github.com/PedroLageTavares/enclosuresensor.git
cd enclosuresensor
```

### 2. Configure secrets

Edit `secrets.yaml` and fill in your Wi-Fi credentials, API key, OTA password, and fallback AP password.

> Replace every `REPLACE_WITH_…` value before flashing. Never commit real credentials.

### 3. Flash

```bash
# First flash (USB)
esphome run enclosuresensor.yaml

# Subsequent updates (OTA)
esphome run enclosuresensor.yaml
```

### 4. Add to Home Assistant

ESPHome will auto-discover the device. Accept the integration in **Settings → Devices & Services → ESPHome**.

## Entities created in Home Assistant

| Entity | Type | Description |
|---|---|---|
| `sensor.temperature` | Sensor | Ambient temperature (°C) |
| `sensor.humidity` | Sensor | Relative humidity (%) |
| `sensor.voc_index` | Sensor | VOC index 0–500 |
| `sensor.acceleration_x/y/z` | Sensor | Per-axis acceleration (g) |
| `sensor.vibration_magnitude` | Sensor | Combined acceleration magnitude (g) |
| `binary_sensor.vibration_detected` | Binary sensor | `ON` when magnitude > 1.2 g |

## Tuning the vibration threshold

The threshold is set in `enclosuresensor.yaml`:

```yaml
return id(vibration_magnitude).state > 1.2f;
```

Increase the value for noisier environments; decrease it for more sensitive detection.

## License

GNU General Public License v3.0 — see [LICENSE](LICENSE).
