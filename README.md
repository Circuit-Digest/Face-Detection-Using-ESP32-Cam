# 🎯 Face Detection Using ESP32-CAM with CircuitDigest Cloud API

<p align="center">
  <img src="https://img.shields.io/badge/Platform-ESP32--CAM-blue?style=for-the-badge&logo=espressif" />
  <img src="https://img.shields.io/badge/AI-CircuitDigest%20Cloud-green?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Language-C%2B%2B%20(Arduino)-orange?style=for-the-badge&logo=arduino" />
  <img src="https://img.shields.io/badge/Protocol-HTTPS-red?style=for-the-badge" />
  <img src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge" />
</p>

<p align="center">
  A real-time <strong>AI-powered face detection system</strong> built with an <strong>ESP32-CAM</strong> module and the <strong>CircuitDigest Cloud API</strong>. Detects faces and returns the count with confidence values — no ML training, no complex setup required!
</p>

---

## 📌 Table of Contents

- [Overview](#-overview)
- [How It Works](#-how-it-works)
- [Components Required](#-components-required)
- [Circuit Diagram](#-circuit-diagram)
- [Getting Started](#-getting-started)
  - [Step 1: Create a CircuitDigest Cloud Account](#step-1-create-a-circuitdigest-cloud-account)
  - [Step 2: Get Your API Key & Test Virtually](#step-2-get-your-api-key--test-virtually)
  - [Step 3: Hardware Setup & Code Upload](#step-3-hardware-setup--code-upload)
- [Code Explanation](#-code-explanation)
- [Output](#-output)
- [Advantages & Limitations](#-advantages--limitations)
- [Troubleshooting](#-troubleshooting)
- [FAQ](#-faq)
- [Relevant Links](#-relevant-links)
- [License](#-license)

---

## 🌍 Overview

Have you ever watched a movie where a system instantly detects a face at a security door and thought *"This looks too complex to build in real life"?* With the **ESP32-CAM** and **CircuitDigest Cloud**, that movie-like system is now surprisingly simple and accessible.

This project builds a fully working **face detection system** — no external camera, no bulky setup, no ML training. Just upload the code, press a button, and the device captures an image, sends it to the cloud, and returns the **number of detected faces** along with **confidence values** for each detection.

> **Press a button → Capture image → Cloud AI detects faces → Count & confidence shown on Serial Monitor**

---

## ⚙️ How It Works

```
[ ultrasonic sensor detects motion ]
        ↓
[ ESP32-CAM Captures Image ]
        ↓
[ Image Sent via Wi-Fi over HTTPS ]
        ↓
[ CircuitDigest Cloud API Processes Image with AI Face Detection ]
        ↓
[ Result Returned: Number of Faces + Confidence Values ]
        ↓
[ Output Displayed on Serial Monitor ]
       ↓
[ the annotated image is sent ot whatsapp with details ]

```

> **Tip:** For testing, you don't need a live subject — any image from the web with clearly visible faces will also work! Always ensure good lighting for best detection accuracy.

---

## 🧰 Components Required

| S.No | Component | Purpose |
|------|-----------|---------|
| 1 | ESP32-CAM | Microcontroller with built-in camera & Wi-Fi |
| 2 | ultrasonic | Triggers image capture when motion is detected |
| 3 | Breadboard | Simplifies and organizes circuit connections |
| 4 | USB-to-Serial (FTDI) Adapter *(if needed)* | For programming standard ESP32-CAM without onboard USB |
| 5 | USB Cable | Powers the system via laptop/PC |

> **⚠️ Note:** If you are using the standard ESP32-CAM (without onboard USB), you need a **USB-to-Serial (FTDI) adapter** for programming:
> - FTDI **TX** → ESP32-CAM **RX** (U0R)
> - FTDI **RX** → ESP32-CAM **TX** (U0T)
> - **GND** → **GND**
> - Hold **GPIO0 LOW** during upload to enter flash mode.

---


## 🚀 Getting Started

### Step 1: Create a CircuitDigest Cloud Account

Go to the [CircuitDigest Cloud website](https://circuitdigest.cloud), create a free account, and log in. Scroll down on the dashboard and click on the **Face Detection** feature.

---

### Step 2: Get Your API Key & Test Virtually

- Your **API Key** will be displayed on the left panel of the Face Detection page.
- Adjust the **confidence level** based on your accuracy requirements.
- Use the **"Try API"** feature to test before connecting hardware:
  1. Upload an image where faces are clearly visible.
  2. Click **"Run Test"**.
  3. The system will return the **detected face count** within seconds.

> 📊 **API Limits:** 15 requests/day and 100 requests/month on the free tier. Each "Try API" test counts toward this limit.

---

### Step 3: Hardware Setup & Code Upload

1. Connect all components as per the circuit diagram.
2. Open **Arduino IDE** and install the **ESP32 board package**.
3. Open the project sketch and fill in your credentials:

```cpp
const char* WIFI_SSID  = "Your_WiFi_SSID";
const char* WIFI_PASS  = "Your_WiFi_Password";
const char* API_KEY    = "Your_API_Key_Here";
```

4. Select **AI Thinker ESP32-CAM** as the board in Arduino IDE.
5. Upload the code (hold **GPIO0 LOW** if using FTDI adapter).
6. Open **Serial Monitor** at **115200 baud**.
7. Press the push button — the face detection result appears within seconds!

---
---



## ✅ Advantages & Limitations

| S.No | Advantages | Limitations |
|------|------------|-------------|
| 1 | Real-time face detection within seconds | Cannot work without cloud API access |
| 2 | Low-cost system using ESP32-CAM with built-in camera & Wi-Fi | Requires an active internet connection |
| 3 | No expensive hardware or powerful processors needed | Blurry images may produce incorrect results |
| 4 | Fully wireless communication without extra modules | Limited by daily/monthly API usage limits |
| 5 | Small size and portable design | Captures single images, not continuous live video |

> **Why CircuitDigest Cloud over alternatives like Edge Impulse?**
> Platforms like Edge Impulse require dataset collection, model training, optimization, and deployment — which is time-consuming. CircuitDigest Cloud provides a **ready-to-use API** that eliminates all of that, enabling faster development and immediate results.

---

## 🛠️ Troubleshooting

### 🔄 Issue 1: ESP32-CAM Restarting Continuously
- **Cause:** Unstable or insufficient power supply.
- **Fix:** Use a proper **5V regulated external power source**. Avoid relying on weak USB connections.

### 🔇 Issue 2: No Output in Serial Monitor
- **Cause:** Incorrect COM port or baud rate.
- **Fix:** Set baud rate to **115200**, verify the correct COM port in Arduino IDE, and check the USB cable and board connection.

### 😶 Issue 3: Face Detection Not Working
- **Cause:** Poor image quality or insufficient lighting.
- **Fix:** Ensure the environment has **proper lighting** and faces are **clearly visible** in front of the camera.

### 🌐 Issue 4: API Connection Error or Timeout
- **Cause:** Network issue, incorrect API key, or HTTPS misconfiguration.
- **Fix:** Verify the internet connection, double-check the **API key**, and ensure HTTPS is correctly configured in the code.

### 🔢 Issue 5: Incorrect Detection Count
- **Cause:** Low confidence threshold or image noise.
- **Fix:** Adjust the **confidence level** in the CircuitDigest Cloud dashboard and use clearer, well-lit images for better accuracy.

---

## ❓ FAQ

**1. Can this system work without the internet?**
> No. The system requires an active internet connection because all image processing is performed on the cloud. Without it, the ESP32-CAM cannot send data to the API.

**2. How accurate is the face detection system?**
> Accuracy depends on lighting conditions, camera angle, and image clarity. Better lighting and clear face visibility will significantly improve detection performance.

**3. What are the limitations of this system?**
> The system depends on internet connectivity and API usage limits. It may also produce incorrect results if faces are partially visible or the image quality is poor.

**4. Can multiple faces be detected at the same time?**
> Yes! The system can detect multiple faces in a single image and return the total count with individual confidence scores. Accuracy improves when faces are clearly visible.

**5. Can this system be used for face recognition?**
> No. This project performs **face detection only** — detecting the presence and count of faces. Face **recognition** (identifying specific individuals) requires additional models and processing beyond the scope of this project.

**6. How can the system be improved?**
> The system can be enhanced by:
> - Adding an **OLED/LCD display** for on-device output
> - Integrating with a **mobile app or cloud dashboard**
> - Adding **email/SMS alerts** when faces are detected
> - Connecting to a **door lock or security system**
> - Logging detection events with timestamps

---

## 🔗 Relevant Links

- 📦 **GitHub Repository:** [Circuit-Digest/Face-Detection-Using-ESP32-Cam](https://github.com/Circuit-Digest/Face-Detection-Using-ESP32-Cam)
- ☁️ **CircuitDigest Cloud:** [circuitdigest.cloud](https://circuitdigest.cloud)
- 🤖 [ESP32-CAM Face Recognition using Edge Impulse](https://circuitdigest.com/microcontroller-projects/esp32-cam-face-recognition-using-edge-impulse)
- 🔐 [ESP32-CAM Face Recognition Door Lock System](https://circuitdigest.com/microcontroller-projects/esp32-camface-recognition-door-lock-system)
- 📋 [Attendance System using ESP32-CAM](https://circuitdigest.com/microcontroller-projects/attendance-system-using-esp32-cam-development-board)

---

<p align="center">
  Made with ❤️ by <a href="https://circuitdigest.com">CircuitDigest</a> | Powered by <a href="https://circuitdigest.cloud">CircuitDigest Cloud AI</a>
</p>
