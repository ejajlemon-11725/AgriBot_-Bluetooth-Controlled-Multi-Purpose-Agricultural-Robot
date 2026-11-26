# 🌱 AgriBot: Bluetooth-Controlled Multi-Purpose Agricultural Robot

> **One robot, many field tasks.** A low-cost, Arduino-based farming robot that ploughs, sows seeds, irrigates and sprays pesticide, all controlled from an Android phone over Bluetooth.

**Project group:** **GreenPulse Robotics**

**Presented by:** **Ejaj Ahmmod Lemon** **(Reg. ID: 23101160)**

---

## 📖 Overview

Agriculture employs roughly 40–45% of Bangladesh's labor force and contributes about 11–12% of GDP, yet much of the work is still manual, slow and physically demanding. Farmers also face direct exposure to toxic pesticides, and most rely on several separate, non-integrated tools.

**AgriBot** addresses this with a single, versatile robot platform. One chassis carries swappable attachments for ploughing, seed sowing, irrigation and pesticide spraying. The farmer drives it and triggers each task from a custom Android app, from a safe distance.

## ❗ Problem Statement

| Challenge | Impact |
|---|---|
| Labor-intensive field operations | ~24–25M workers do heavy physical work by hand |
| Inefficient irrigation and spraying | ~18–22M workers; wasted water and chemicals, lower yield |
| Farmer safety | 15–20M farmers exposed to toxic chemicals during manual spraying |
| Fragmented tooling | Over 85% of landholders depend on multiple non-integrated manual tools |

## ✨ Features

- 📱 **Wireless control**: operate the robot from a custom Android app via an HC-05 Bluetooth module.
- 🚜 **Ploughing**: a plough attachment, combined with soil-moisture sensing.
- 🌾 **Seed sowing**: a sowing mechanism for accurate seed placement and spacing.
- 💧 **Irrigation**: a water pump and sprinkler for controlled watering.
- 🧪 **Pesticide spraying**: the same pump and sprinkler system, operated remotely so the farmer avoids chemical exposure.
- 🌡️ **Smart soil monitoring**: a soil-moisture sensor gives real-time readings. If moisture is low the pump is switched on; otherwise it stays off, which prevents over-watering.
- 🔧 **Modular design**: swappable attachments avoid the cost of buying separate machines.
- 🛡️ **Safe operation**: control from a distance keeps farmers away from pesticides.

> **Ploughing and sensing in one:** if the soil-moisture sensor is mounted at a 45° angle, it can sense moisture and work as a plough at the same time.

## 🧩 System Architecture

The embedded system follows an **Input → Processing → Output** model.

| Stage | Components |
|---|---|
| **Input** | Android smartphone app, HC-05 Bluetooth module, soil-moisture sensor |
| **Processing** | Arduino Uno: receives and decodes commands, controls mobility, processes soil feedback, runs the task sequences |
| **Output** | 4× DC geared motors (via L298N driver), water pump and sprinkler (via relays), seed-sower mechanism, status indicators |

### Workflow

```
Start / Initialize
   → Connect Android app (Bluetooth)
   → Manual command input
   → Arduino receives and processes command
   → Ploughing + soil-moisture monitoring
        ├─ Low moisture      → Activate irrigation (pump ON)
        └─ Sufficient moisture → Skip irrigation (pump OFF)
   → Task execution: Ploughing | Seed sowing | Irrigation | Pesticide spraying
   → Monitoring and control (send status to app)
   → Task completed → standby / wait for next command
```

### Control logic (pseudocode)

```text
START
INITIALIZE
CONNECT Android app
WHILE system active DO
    WAIT for manual command
    RECEIVE command from Android app
    PROCESS command

    IF ploughing selected THEN
        START ploughing
        READ soil moisture
        IF soil moisture is low THEN START irrigation
        ELSE KEEP pump OFF
        STOP ploughing
    ELSE IF seed sowing selected THEN
        START seed sowing
        CONTROL seed placement
        STOP seed sowing
    ELSE IF irrigation selected THEN
        START water pump and sprinkler
        PERFORM irrigation
        STOP water pump and sprinkler
    ELSE IF pesticide spraying selected THEN
        START spraying mechanism
        PERFORM pesticide spraying
        STOP spraying mechanism
    ELSE
        DISPLAY invalid command
    END IF

    MONITOR system status
    SEND status to Android app
    SAVE task status
END WHILE
RETURN to standby mode
END
```

## 🔩 Hardware Components

| Category | Component |
|---|---|
| Microcontroller | Arduino Uno |
| Wireless communication | HC-05 Bluetooth module |
| User interface | Android smartphone app |
| Sensing | Capacitive soil-moisture sensor |
| Power switching | Relay modules |
| Motor driver | L298N |
| Mobility | 4× DC geared motors |
| Structure | PVC board chassis |
| Power | Rechargeable battery pack |
| Mechanisms | Seed sower, water pump + sprinkler |

The wiring diagram (made in Cirkit Designer) is in [`/docs/circuit-diagram`](docs/) *(add your exported image here)*.

## 💰 Estimated Prototype Cost

| Component | Estimated cost (BDT) |
|---|---|
| Arduino Uno and HC-05 module | ≈ ৳ 950 |
| L298N driver and 4× DC motors | ≈ ৳ 950 |
| PVC board and battery | ≈ ৳ 1,100 |
| Seed sower, pump, sprinkler, relays, sensors | ≈ ৳ 1,100 |
| **Total hardware cost** | **≈ ৳ 4,100** |

*Component cost only. Excludes chassis fabrication, custom wiring and labor. An existing Android device is assumed.*

## 🚀 Getting Started

> Add the exact pin mappings, library versions and app file once they are finalized in your build.

### Prerequisites
- Arduino IDE
- An Android smartphone (Bluetooth)
- All hardware components listed above, assembled per the circuit diagram

### Setup
1. **Assemble the hardware.** Build the PVC chassis, mount the 4 DC motors, and wire the L298N, relays, soil sensor and HC-05 to the Arduino Uno as shown in the circuit diagram.
2. **Upload the firmware.** Open the sketch in the Arduino IDE, select **Arduino Uno** and the correct port, and upload it.
3. **Install the Android app.** Install the AgriBot control app on your phone.
4. **Pair Bluetooth.** Pair your phone with the **HC-05** module (default PIN is usually `1234` or `0000`).
5. **Power on and connect.** Switch on the battery pack, open the app and connect to the robot.
6. **Operate.** Use the directional controls to drive, and choose **Ploughing**, **Seed Sowing**, **Irrigation** or **Pesticide Spraying** from the app.

## 🗺️ Implementation Roadmap

1. **Research**: requirement analysis and component selection
2. **Hardware**: chassis build and drive-motor wiring
3. **Software**: app development and Bluetooth integration
4. **Assembly**: attaching the plough, sower and sprayer
5. **Testing**: field calibration and final demo

## ⚖️ Advantages and Limitations

**Advantages**
- Cost-effective compared with buying separate machines
- Reduces manual labor and health risks
- Multi-purpose, swappable attachments
- Safe remote operation from a mobile phone

**Current limitations**
- Bluetooth range is limited to about 10 m
- Limited battery life

## 🔭 Future Scope

- GPS-guided autonomous navigation
- Solar charging for extended operation

## 📁 Suggested Repository Structure

```
AgriBot/
├── firmware/          # Arduino sketch(es)
├── android-app/       # App source or APK
├── docs/              # Circuit diagram, workflow diagram, presentation
├── images/            # Photos and screenshots
└── README.md
```

## 🙏 Acknowledgements

We sincerely thank **Nazmun Nahid**, Assistant Professor, **University of Asia Pacific**, for her valuable guidance, support and encouragement throughout this project.

## 👤 Author

**Ejaj Ahmmod Lemon**, Reg. ID 23101160
Project Group: **GreenPulse Robotics**

## 📄 License

Add a license of your choice (for example MIT) before publishing.
