# Morse Code Decoder

A handheld Morse code learning device built on the RP2040 Zero with an SSD1306 OLED display. Press the button in Morse code patterns and the decoded character displays on screen. Built from salvaged and low-cost components, battery powered, and housed in a custom 3D printed ABS enclosure with a laser-etched Morse code reference chart.

---

## Parts List

| Part | Notes |
|------|-------|
| Waveshare RP2040 Zero | Main microcontroller |
| SSD1306 0.96" OLED 128x64 I2C | 4-pin, GND/VDD/SCK/SDA |
| Momentary tactile push button | 4-pin SMD or through-hole |
| LiPo battery ~100mAh | 3.7V nominal |
| LiPo charging module | TP4056 or equivalent |
| Toggle switch | For power |
| 3D printed ABS enclosure | Custom or adapted from Bambu Labs library |
| M2 screws | 4x for enclosure |
| Wire | 28AWG recommended |

---

## Wiring

### OLED (SSD1306 I2C)

| OLED Pin | RP2040 Zero Pin |
|----------|----------------|
| GND | GND |
| VDD | 3.3V |
| SCK | GP5 |
| SDA | GP4 |

### Button

| Button Pin | RP2040 Zero Pin |
|------------|----------------|
| Pin 1 | GP15 |
| Pin 2 | GND |

### Power
- LiPo battery → charging module → toggle switch → RP2040 Zero 5V/GND
- USB-C on the Zero for programming and charging

---

## Software Setup

### Flash MicroPython

1. Download the MicroPython UF2 for RP2040 from [micropython.org/download/RPI_PICO](https://micropython.org/download/RPI_PICO/)
2. Hold the BOOT button on the Zero while plugging into USB
3. It mounts as a drive called RPI-RP2
4. Drag and drop the UF2 file onto the drive
5. The board reboots automatically into MicroPython

### Install SSD1306 Library

1. Open [Thonny](https://thonny.org) and set interpreter to MicroPython (Raspberry Pi Pico) on the correct COM port
2. Go to [raw.githubusercontent.com/micropython/micropython-lib/master/micropython/drivers/display/ssd1306/ssd1306.py](https://raw.githubusercontent.com/micropython/micropython-lib/master/micropython/drivers/display/ssd1306/ssd1306.py)
3. Copy the contents
4. In Thonny, create a new file, paste the contents, and save it to the device as `ssd1306.py`

### Upload Main Code

1. Copy `main.py` from this repo into Thonny
2. Save it to the device as `main.py`
3. The device will run it automatically on every boot

---

## Usage

- **Tap** the button in Morse code patterns
- The current sequence (dots and dashes) shows in the top left
- After a short pause the character is decoded and displayed large in the center
- Decoded text accumulates at the bottom of the screen
- **Hold 2 seconds** to clear everything and start over

### Timing

| Parameter | Value |
|-----------|-------|
| Dot max duration | 170ms |
| Dash min duration | 170ms+ |
| Letter gap | 500ms |
| Word gap | 1500ms |
| Long press clear | 2000ms |

These values are tuned for a natural learning pace. Adjust `DOT_MAX`, `LETTER_GAP`, and `WORD_GAP` in `main.py` to suit your rhythm.

### Display Layout

```
[ current sequence     ]
────────────────────────
          A             
────────────────────────
[ decoded text history ]
```

---

## Enclosure

Designed for the Waveshare RP2040 Zero form factor. Printed in ABS on a Bambu Labs H2D. The front face has a laser-etched Morse code reference chart visible at an angle — subtle enough to be a reference rather than a crutch.

---

## Roadmap

- **v2**: HID keyboard mode over USB — plug into any device and decoded characters are typed as keystrokes. No drivers, no configuration. Long press menu for TX / clear / cancel.

---

## License

MIT
