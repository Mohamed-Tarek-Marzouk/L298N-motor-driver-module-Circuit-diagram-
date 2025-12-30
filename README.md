# 📁 L298N Motor Driver Module – Custom Circuit Design

![Project Status](https://img.shields.io/badge/Status-Completed-success)
![Category](https://img.shields.io/badge/Category-Hardware_Design-blue)

## 📌 Overview
This project involves designing a custom motor driver circuit based on the **L298N dual H-Bridge IC**. The primary goal is to control two DC motors via a microcontroller, incorporating essential protection features and a regulated power supply. 

The circuit is designed to safely interface with various microcontrollers such as **ATmega32, Arduino, and STM32**.

---

## 🧩 Components Used

| Component | Quantity | Description |
| :--- | :---: | :--- |
| **L298N Motor Driver IC** | 1 | Dual full-bridge driver for controlling two DC motors. |
| **7805 Voltage Regulator** | 1 | Provides regulated 5V from external power supply. |
| **1N4007 Diodes** | 8 | Flyback diodes to protect the L298N from motor back-EMF. |
| **LED** | 1 | Power status indicator. |
| **Resistor (330Ω–1kΩ)** | 1 | Current limiting resistor for the status LED. |
| **3-Pin Screw Terminal** | 1 | External power input: GND, +5V, VCC (motor power). |
| **2-Pin Screw Terminals** | 2 | For connecting Motor A and Motor B. |
| **6-Pin Socket Header** | 1 | Microcontroller interface (ENA, IN1, IN2, IN3, IN4, ENB). |
| **2-Pin Jumper Socket** | 1 | To optionally bridge +5V logic and +5V motor power. |

---

## ⚙️ Circuit Description

### 🔌 Power Supply Section
A 3-pin screw terminal handles the following connections:
* **GND:** Common Ground.
* **+5V (Logic):** Can be supplied from the microcontroller or the onboard 7805 regulator.
* **VCC (Motor Power):** Input for motors (typically 6V to 12V).

The **7805 regulator** steps down VCC to 5V for logic circuits. A **2-pin jumper** allows you to choose between shared or isolated logic power.

### 🚦 Indicator LED
A status LED is connected across the regulated 5V and GND with a current-limiting resistor to provide visual confirmation of power.

### 🧠 L298N Control Logic
The L298N IC is controlled via 6 pins:
* **ENA / ENB:** Enable/Disable motors (Supports **PWM** for speed control).
* **IN1, IN2 / IN3, IN4:** Direction control pins for Motor A and Motor B respectively.

### 🛡️ Protection Mechanism
Eight flyback diodes are placed across the output pins (**OUT1–OUT4**) to safeguard the IC against inductive voltage spikes and back-EMF from the motors.

---

## 🔗 Microcontroller Interface

| Pin on Socket | Function | Notes |
| :--- | :--- | :--- |
| **ENA** | Enable Motor A | Use PWM for Speed Control |
| **IN1** | Motor A Direction 1 | Digital High/Low |
| **IN2** | Motor A Direction 2 | Digital High/Low |
| **IN3** | Motor B Direction 1 | Digital High/Low |
| **IN4** | Motor B Direction 2 | Digital High/Low |
| **ENB** | Enable Motor B | Use PWM for Speed Control |

---

## 📝 Important Notes

> [!IMPORTANT]
> **Common Ground:** If you are using separate power supplies for the logic and the motors, always ensure they share a **Common Ground (GND)**.

* **Heat Management:** Always use a heatsink on the L298N IC if your motors have a high current demand to prevent overheating.
* **Jumper Usage:** * **Closed Jumper:** Shared supply (Logic 5V is powered by the 7805 from VCC).
    * **Open Jumper:** Isolated supply (Logic 5V must be provided externally).
* **Voltage Rating:** Double-check your motor's voltage requirements before connecting them to the VCC terminal.
