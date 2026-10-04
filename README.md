# 🧤 Smart Glove: Sign Language to Speech

A wearable smart glove that translates hand gestures into spoken phrases, with no phone or computer needed. Built as a graduation project in Computer and Communication Engineering.

## 🎯 Problem
Most people don't understand sign language, which creates a communication barrier for deaf and speech-impaired people. This project aims to help bridge that gap with a low-cost, standalone device.

## ⚙️ How It Works
1. **5 flex sensors** measure the bending of each finger.
2. **MPU6050** (accelerometer + gyroscope) captures hand orientation and motion.
3. **ESP32** reads all sensors and compares the values against calibrated ranges for each gesture (threshold-based classification with sensor fusion).
4. **DFPlayer Mini** plays the matching pre-recorded phrase through a speaker.

## 🤟 Supported Gestures
| Gesture | Spoken Output |
|---------|---------------|
| OK | "OK" |
| Stop | "Stop" |
| No | "No" |
| I am hungry | "I am hungry" |
| I have a question | "I have a question" |

## 🔧 Hardware
| Component | Purpose |
|-----------|---------|
| ESP32 | Main microcontroller |
| 5x Flex sensors | Finger bend detection |
| MPU6050 | Hand orientation and motion |
| DFPlayer Mini + microSD | Audio playback |
| Speaker | Voice output |
| Rechargeable battery / power bank | Power |
| Fixed resistors | Voltage dividers for the flex sensors |

## 🔌 Wiring
Add your wiring diagram or circuit photo here: `images/circuit.jpg`

## 💻 Software
- Arduino IDE
- Library: `Adafruit MPU6050` (and `Adafruit Unified Sensor`)
- Library: `DFRobotDFPlayerMini`

## 🚀 Setup
1. Wire the components as shown in the diagram.
2. Copy the audio files to the microSD card (FAT32) with names `0001.mp3`, `0002.mp3`, ...
3. Open `code/smart_glove.ino` in Arduino IDE.
4. Select your ESP32 board and upload.
5. Calibrate the flex sensor ranges (see below).

## 🎚️ Calibration
Flex sensor values vary between sensors and users, so each sensor's range is set individually from serial monitor readings. Gesture ranges are defined in the code.

## 🔮 Future Improvements
- More gestures and full sentences
- Wireless communication
- More advanced recognition algorithms

## 📄 Report
Full project report: [docs/Graduation_Project_Report.pdf](docs/Graduation_Project_Report.pdf)

## 👤 Author : Saba Amaireh
Computer and Communication Engineering graduate
[LinkedIn](www.linkedin.com/in/sabaamaireh)
