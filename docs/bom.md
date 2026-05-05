# Bill of Materials

## Core electronics

| Item | Qty | Notes |
|---|---:|---|
| Seeed Studio XIAO ESP32-C3 | 1 | Main controller |
| Grove Base for XIAO | 1 | Simplifies sensor wiring |
| SGP41 VOC/NOx sensor | 1 | Air quality trend sensor |
| LIS3DH accelerometer | 1 | Printer activity detection |
| AHT20 sensor | 1 | Humidity and temperature compensation source |
| BMP280 sensor | 1 | Pressure monitoring |
| 0.96 inch OLED (SSD1315 or SSD1306-compatible, I2C) | 1 | Local status display |
| MP1584EN buck converter | 1 | 12V to 5V conversion |
| IRLB8721 MOSFET (optional) | 1 | Reserved for future fan control |

## Power and wiring

| Item | Qty | Notes |
|---|---:|---|
| 12V DC input source | 1 | Match expected current budget |
| Hook-up wire set | 1 | Prefer flexible stranded wire |
| JST/Dupont connectors (as needed) | As needed | Match module connectors |
| Heat shrink tubing | Assorted | Insulation and strain relief |

## Mechanical and assembly

| Item | Qty | Notes |
|---|---:|---|
| Enclosure | 1 | Ventilated but dust-protected |
| Standoffs/spacers | As needed | Keep boards mechanically stable |
| M2/M3 screws and nuts | Assorted | For mounting |

## Notes

- Keep MOSFET control unpopulated unless fan control is implemented.
- Validate sensor breakout voltage compatibility before final assembly.
- Keep a spare sensor cable and one spare XIAO board for faster maintenance.
