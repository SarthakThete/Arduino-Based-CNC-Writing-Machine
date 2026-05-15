# ✍️ Arduino UNO Writing Machine (CNC Pen Plotter)

A DIY pen plotter / writing machine built using an **Arduino UNO**, **CNC Shield**, **stepper motors** for X & Y axes, and a **servo motor** for the Z axis (pen up/down). G-code is generated using **Inkscape** and sent via **Universal G-code Sender (UGS)**.

---

## 📸 Project Overview

This project is a low-cost CNC writing machine capable of drawing designs, writing text, and plotting vector graphics on paper. It converts any SVG design into G-code and physically draws it using a pen.

---

## 🔧 Hardware Used

| Component | Details |
|---|---|
| Microcontroller | Arduino UNO |
| Motor Driver Shield | CNC Shield V3 |
| X & Y Axis Motors | Stepper Motors (NEMA 17 or 28BYJ-48) |
| Z Axis (Pen Up/Down) | Servo Motor (SG90) |
| Power Supply | 12V DC Adapter |
| Frame | DIY / 3D Printed |
| Pen Holder | Custom mount |

---

## 💻 Software Used

| Software | Purpose |
|---|---|
| [Arduino IDE](https://www.arduino.cc/en/software) | Upload GRBL firmware |
| [GRBL Library](https://github.com/grbl/grbl) | CNC motion control firmware |
| [Inkscape](https://inkscape.org/) | Design creation + G-code export |
| [Inkscape G-code Extension](https://github.com/martymcguire/inkscape-unicorn) | SVG to G-code conversion |
| [Universal G-code Sender (UGS)](https://universalgcodesender.com/) | Send G-code to Arduino |

---

## ⚙️ How It Works

1. **Design** your text or image in **Inkscape** as an SVG
2. **Export G-code** using the Inkscape G-code extension (gcodetools / J Tech Photonics plugin)
3. **Upload GRBL firmware** to Arduino UNO via Arduino IDE
4. **Connect** the machine and open **Universal G-code Sender**
5. **Load and send** the G-code file — the machine draws it!

---

## 🔌 Wiring / Pin Connections

| Component | CNC Shield / Arduino Pin |
|---|---|
| X-axis Stepper | X driver slot on CNC Shield |
| Y-axis Stepper | Y driver slot on CNC Shield |
| Servo Motor (Z-axis) | Pin 11 (or Z+ on shield) |
| CNC Shield | Plugged directly onto Arduino UNO |

> ⚠️ **Note:** A non-original (clone) Arduino UNO was used in this project. This caused only the Y-axis to respond correctly. If using a clone board, ensure proper driver compatibility and check CH340 USB driver installation.

---

## 📂 Repository Structure

```
📁 arduino-writing-machine/
│
├── README.md               ← This file
├── /gcode-samples/         ← Sample .gcode files for testing
├── /images/                ← Photos of the build
└── /docs/                  ← Project report and diagrams
```

---

## 🚀 Getting Started

### Step 1 — Flash GRBL to Arduino
1. Download [GRBL from GitHub](https://github.com/grbl/grbl)
2. Open Arduino IDE → Sketch → Include Library → Add .ZIP Library → select grbl
3. Open: `File → Examples → grbl → grblUpload`
4. Select your board (Arduino UNO) and port
5. Upload!

### Step 2 — Prepare G-code in Inkscape
1. Install Inkscape G-code extension
2. Create your design/text as a path (`Object to Path`)
3. Go to `Extensions → Generate from Path → G-code Tools`
4. Export the `.gcode` file

### Step 3 — Send G-code
1. Open **Universal G-code Sender**
2. Connect to Arduino (baud rate: **115200**)
3. Load your `.gcode` file
4. Click **Send** and watch it draw!

---

## ⚠️ Known Issues & Limitations

- **Clone Arduino UNO:** Using a non-genuine Arduino may cause axis communication issues (only Y-axis worked in initial testing). Install the correct CH340 driver for clone boards.
- **Z-axis calibration:** Servo angles for pen-up and pen-down positions need to be tuned in GRBL settings.
- **Speed & accuracy:** Low-cost stepper motors may skip steps at high speeds. Keep feed rate low (~300–500 mm/min).

---

## 🛠️ GRBL Configuration Tips

Open UGS console and type these commands:

```
$100=80   (X steps/mm)
$101=80   (Y steps/mm)
$110=500  (X max speed mm/min)
$111=500  (Y max speed mm/min)
$27=1     (Homing pull-off)
```

For servo Z-axis, GRBL uses spindle PWM to control the servo. Tune:
- `$30` = max servo value (pen down)
- `$31` = min servo value (pen up)

---

## 📖 References

- [GRBL GitHub](https://github.com/grbl/grbl)
- [Universal G-code Sender](https://universalgcodesender.com/)
- [Inkscape](https://inkscape.org/)
- [CNC Shield Pinout](https://blog.protoneer.co.nz/arduino-cnc-shield/)

---

## 👤 Author

Made with ❤️ as a DIY hobby project.
Feel free to fork, improve, and share!

---

## 📄 License

This project is open-source under the [MIT License](LICENSE).
