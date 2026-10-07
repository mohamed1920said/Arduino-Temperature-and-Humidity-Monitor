# Arduino Temperature and Humidity Monitor

An Arduino-based room monitor that reads temperature and relative humidity from a DHT11 sensor and displays both measurements on a 16x2 parallel LCD. The same values are also written to the serial monitor for debugging.

## Repository contents

- `dht11+lcd.txt` - Arduino sketch source. It is stored as a text file and must be copied into an `.ino` sketch before uploading with the Arduino IDE.
- `rapport.pdf` - project report with the hardware description, wiring illustration, and prototype results.
- `PHOTO-2025-02-12-16-00-27.jpg` - photograph of the assembled prototype.

## Hardware and libraries

The report and source describe the following setup:

- Arduino Uno or a compatible 5 V Arduino board
- DHT11 temperature/humidity sensor
- HD44780-compatible 16x2 LCD in 4-bit parallel mode
- 10 kOhm potentiometer for LCD contrast
- Breadboard, jumper wires, and a suitable USB/power source
- A compatible Arduino `DHT.h` library
- Arduino `LiquidCrystal` library

## Pin map

| Device signal | Arduino pin |
| --- | --- |
| DHT11 data | D7 |
| LCD RS | D12 |
| LCD Enable | D11 |
| LCD D4 | D5 |
| LCD D5 | D4 |
| LCD D6 | D3 |
| LCD D7 | D2 |

Connect all grounds together. Wire LCD power, contrast, and backlight according to the LCD module's datasheet; those connections are not represented in the source code.

## Run the project

1. Install the Arduino IDE and the DHT sensor library required by `DHT.h`.
2. Create a new Arduino sketch and copy the contents of `dht11+lcd.txt` into its `.ino` file.
3. Assemble the DHT11 and LCD using the pin map above and the wiring diagram in `rapport.pdf`.
4. Select the correct board and serial port, then compile and upload the sketch.
5. Open the serial monitor at **9600 baud**.

After a two-second startup message, the program reads the sensor approximately once per second. The first LCD row shows temperature in degrees Celsius and the second shows relative humidity. If either reading is invalid, the LCD shows `Erreur lecture!` and the next loop tries again.

## Notes and limitations

- A source comment says that measurements are two seconds apart, but the implemented loop delay is one second.
- DHT11 sensors have limited range, accuracy, and update rate. This project is appropriate for learning and general room monitoring, not calibrated measurement or safety control.
- The display is cleared and redrawn for every sample, which may produce visible flicker on some LCD modules.
- The sketch has no data logging, network connection, or long-term sensor-error handling.
- Verify the sensor module's pin order before applying power; bare DHT11 sensors and breakout modules do not always use the same arrangement.
