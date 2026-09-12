https://www.waveshare.com/esp32-c6-zero.htm?srsltid=AfmBOoqD9-Ih9f1LIh4pihioVcYzxsb1XXMUCX34L-o2pgk6UcKUfQ6J

https://www.az-delivery.de/products/0-96zolldisplay?srsltid=AfmBOoqaQn6z6QT__j0y47mMPDGE2ZBSjMxP150AkAVrUZu7DmX2fmuX

https://grabcad.com/library/arduino-0-91-0-96-inch-oled-1

https://docs.waveshare.com/ESP32-C6-Zero


Batteriefach 
https://www.amazon.de/dp/B00OK6BFGS?ref=ppx_yo2ov_dt_b_fed_asin_title


Gehäuse
https://www.amazon.de/dp/B0F47SKWYW?niid=nl_cl_lst_a_1_1&ref_=nl_cl_lst_a_1_1&nrid=B70AHYF8PZZX1DP8Y8KT&th=1

## KiCad-Bauteilstatus

Die ersten projektspezifischen Footprints liegen in der gemeinsamen Bibliothek
unter `KiCad-Library/Footprints/Modules.pretty`:

| Baugruppe | KiCad-Footprint | Status |
| --- | --- | --- |
| Waveshare ESP32-C6-Zero | `Modules:ESP32-C6-Zero` | erstellt, 23,5 x 18,0 mm, 2,54 mm Raster |
| OLED 0,96 Zoll SSD1306 I2C | `Modules:OLED-0.96-SSD1306-I2C` | erstellt, 4-polig, 2,54 mm Raster |
| DS18B20 Vorlauf/Ruecklauf | `Connector_Generic:Conn_01x03` je Sensor | externer Sensor, kein Board-Footprint erforderlich |

### ESP32-C6-Zero Pad-Reihenfolge

Die Footprint-Pads folgen der physischen Reihenfolge der Herstellerzeichnung.
Die Zuordnung fuer den Schaltplan ist:

- Pad 1..9: `5V`, `GND`, `3V3`, `GPIO0`, `GPIO1`, `GPIO2`, `GPIO3`, `GPIO4`, `GPIO5`
- Pad 10..18: `TX/GPIO16`, `RX/GPIO17`, `GPIO14`, `GPIO15`, `GPIO18`, `GPIO19`, `GPIO20`, `GPIO21`, `GPIO22`

Fuer die Firmware werden `GPIO2` (gemeinsamer OneWire-Datenbus), `GPIO3`
(geschaltete Sensorversorgung/Pull-up), `GPIO9` (BOOT-Taster), `GPIO8`
(RGB-LED) sowie `GPIO18`/`GPIO19` (OLED SDA/SCL) verwendet. GPIO8 und
GPIO9 liegen auf der Rueckseite des Zero-M und sind beim normalen Zero nicht
als herausgefuehrte Pads vorhanden; fuer die aktuelle Zero-Variante sollten
Taster und LED daher ueber die vorhandene Board-Hardware behandelt werden.
