# RespiroSense
### Intelligent Contactless Respiration Monitoring System using ESP32

<p align="center">
  <img src="images/system_overview.png" width="850">
</p>

## Overview

RespiroSense is a real-time embedded respiration monitoring system designed for continuous breathing analysis and abnormal respiration detection using edge AI signal processing techniques.

The system acquires respiratory vibrations through an INMP441 digital MEMS microphone, performs real-time DSP on an ESP32, estimates breathing rate, detects apnea-like conditions, and provides local audio/visual alerts while simultaneously transmitting emergency notifications through Wi-Fi.

The entire application executes on-device without requiring cloud-side signal processing, enabling low-latency operation suitable for healthcare monitoring, elderly care, remote patient observation, and wearable medical research.

---

# Key Features

- Real-time respiration monitoring
- Digital MEMS microphone acquisition (INMP441)
- Noise reduction and digital filtering
- Adaptive peak detection algorithm
- Breathing rate estimation (BPM)
- Apnea / abnormal breathing detection
- OLED live monitoring interface
- Audio alarm using I2S amplifier
- Wi-Fi based emergency notification
- FreeRTOS multi-task architecture
- Low-latency edge processing
- Power optimized embedded firmware

---

# Hardware Architecture

| Component | Purpose |
|------------|---------|
| ESP32 DevKit | Main processing unit |
| INMP441 | Digital MEMS Microphone |
| MPU6050 | Motion detection & false alarm rejection |
| SSD1306 OLED | Live monitoring display |
| MAX98357A | I2S Digital Audio Amplifier |
| 4W Speaker | Emergency audio alert |
| Push Button | Silence / Snooze |
| Wi-Fi | Remote notification |

---

# System Architecture

```
                 INMP441
                     │
             I2S Audio Stream
                     │
             Signal Conditioning
                     │
      Bandpass + Noise Filtering
                     │
       Respiration Signal Extraction
                     │
          Peak Detection Algorithm
                     │
          Breathing Rate Estimation
                     │
        Abnormality Detection Engine
             │                 │
             │                 │
          OLED Display     Audio Alarm
             │                 │
             └────── ESP32 Wi-Fi ──────► Telegram/Web API
```

---

# Firmware Architecture

```
                 FreeRTOS Scheduler
                         │
 ┌──────────────────────────────────────────────────┐
 │                                                  │
 │ Motion Task (MPU6050)                            │
 │                                                  │
 │ Audio Acquisition Task (INMP441)                 │
 │                                                  │
 │ Respiration Processing Task                      │
 │                                                  │
 │ OLED Display Task                               │
 │                                                  │
 │ Alert Management Task                            │
 │                                                  │
 │ Wi-Fi Communication Task                         │
 │                                                  │
 └──────────────────────────────────────────────────┘
```

---

# Signal Processing Pipeline

1. I2S audio acquisition
2. DC offset removal
3. Low-frequency respiration filtering
4. Moving average smoothing
5. Adaptive threshold generation
6. Peak detection
7. Breathing interval calculation
8. BPM estimation
9. Apnea detection
10. Alert generation

---

# GPIO Configuration

| GPIO | Function |
|-------|----------|
| GPIO21 | I2C SDA |
| GPIO22 | I2C SCL |
| GPIO25 | INMP441 WS |
| GPIO26 | INMP441 BCLK |
| GPIO33 | INMP441 Data |
| GPIO27 | MAX98357A BCLK |
| GPIO14 | MAX98357A LRC |
| GPIO32 | MAX98357A DIN |
| GPIO13 | Amplifier Enable |
| GPIO4 | MPU6050 Interrupt |
| GPIO0 | Silence Button |
| GPIO2 | Status LED |

---

# Software Stack

- Embedded C++
- Arduino Framework
- ESP-IDF Drivers
- FreeRTOS
- I2S Driver
- Wire Library
- SSD1306 Graphics Library
- Wi-Fi Library

---

# Design Considerations

- Dual I2S controller utilization
- Mutex-protected shared I2C bus
- Interrupt-safe sensor acquisition
- Modular firmware architecture
- Non-blocking task scheduling
- Deterministic execution
- Low memory footprint
- Low power operation

---

# Applications

- Remote patient monitoring
- Home healthcare
- Elderly monitoring
- Sleep observation
- Smart hospital systems
- Respiratory research
- Embedded healthcare devices
- Wearable medical systems

---

# Repository Structure

```
RespiroSense/
│
├── src/
│   ├── main.cpp
│   ├── audio.cpp
│   ├── motion.cpp
│   ├── display.cpp
│   ├── wifi.cpp
│   ├── alert.cpp
│   └── utilities.cpp
│
├── include/
│
├── images/
│   ├── system_overview.png
│   ├── circuit_diagram.png
│   └── architecture.png
│
├── docs/
│
├── README.md
│
└── LICENSE
```

---

# Performance

| Metric | Value |
|---------|-------|
| Controller | ESP32 Dual-Core |
| Sampling Interface | I2S |
| Display Interface | I2C |
| Processing | Real-time |
| RTOS | FreeRTOS |
| Wireless | Wi-Fi 2.4 GHz |

---

# Future Enhancements

- TinyML respiration classification
- Respiratory waveform visualization
- OTA firmware updates
- BLE companion application
- MQTT integration
- Cloud dashboard
- Long-term health analytics
- Multi-patient monitoring

---

# License

This project is intended for educational, research, and embedded systems development purposes.

---

## Author

**Sivanesh G**

Electronics & Communication Engineering  
Embedded Systems | IoT | Edge AI | Real-Time Firmware | Semiconductor Technologies

*"Building reliable embedded systems where hardware meets intelligent software."*
