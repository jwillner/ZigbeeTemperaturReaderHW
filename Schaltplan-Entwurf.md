# Schaltplan-Entwurf

## Baugruppen

| Ref. | Bauteil | Funktion |
| --- | --- | --- |
| A1 | Waveshare ESP32-C6-Zero | Zigbee, Auswertung und Versorgung |
| J1 | OLED-0.96-SSD1306-I2C | Anzeige |
| J2 | DS18B20 Vorlauf, 3-polig | Temperaturfühler Vorlauf |
| J3 | DS18B20 Rücklauf, 3-polig | Temperaturfühler Rücklauf |
| J4 | Versorgung, 2-polig | externe 3,3-V-Versorgung |
| R1 | 4,7 kOhm | OneWire-Pull-up |
| C1 | 100 nF | lokale Abblockung der Sensorversorgung |

## Netze

| Netz | Anschlüsse |
| --- | --- |
| `+3V3` | J4 `+3V3`, A1 `3V3`, J1 `VCC` |
| `GND` | J4 `GND`, A1 `GND`, J1 `GND`, J2 `GND`, J3 `GND`, C1 `-` |
| `SENSOR_POWER` | A1 `GPIO3`, J2 `VDD`, J3 `VDD`, R1 `1` |
| `ONEWIRE` | A1 `GPIO2`, J2 `DQ`, J3 `DQ`, R1 `2` |
| `OLED_SDA` | A1 `GPIO18`, J1 `SDA` |
| `OLED_SCL` | A1 `GPIO19`, J1 `SCL` |

R1 liegt zwischen `SENSOR_POWER` und `ONEWIRE`. C1 liegt zwischen
`SENSOR_POWER` und `GND` und sollte nahe an den Sensor-Steckverbindern
platziert werden. Die Firmware schaltet `SENSOR_POWER` über GPIO3; deshalb
darf die Sensorversorgung nicht direkt an `+3V3` angeschlossen werden.

## Anschlussreihenfolge

Die vier Pins des OLED-Moduls sind laut Bestückungsfoto von links nach rechts:
`GND`, `VCC`, `SCL`, `SDA`.

Die DS18B20-Steckverbinder werden jeweils als `GND`, `DQ`, `VDD` beschriftet.
Die beiden Sensoren hängen absichtlich am selben OneWire-Bus; die Firmware
unterscheidet sie über ihre ROM-Adressen.

## Versorgung

J4 ist ein einfacher zweipoliger Versorgungseingang. An J4 darf ausschließlich
eine geregelte 3,3-V-Spannung angeschlossen werden. Der Pluspol liegt an
`+3V3`, der Minuspol an `GND`. Eine Batterie darf nicht direkt an J4 liegen,
wenn ihre Spannung über 3,3 V steigen kann; dann ist davor ein geeigneter
Regler erforderlich.