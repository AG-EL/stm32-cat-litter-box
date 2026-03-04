# Automatic Cat Litter Box – STM32 Control System

## Project Overview

This project implements an **automatic cat litter box cleaning system** based on an **STM32 microcontroller**.  
The system detects when a cat enters and leaves the litter box using **PIR motion sensors**, and then automatically performs a cleaning cycle using a **motor-driven rotating mechanism**.

The controller manages the entire cleaning sequence using a **finite state machine (FSM)** and ensures safe operation by monitoring **limit switches** and interrupt signals.

The project demonstrates the use of:

- STM32 GPIO
- External interrupts (EXTI)
- PWM motor control
- UART communication
- Finite State Machine architecture

---

## Hardware Components

Main hardware used in the system:

- STM32 microcontroller
- L293D motor driver
- DC motor
- Two PIR motion sensors
  - outside sensor (detects cat approaching)
  - inside sensor (detects cat inside litter box)
- Two limit switches
  - 0° position
  - 180° position
- HM-10 BLE module
- UART communication
- PWM motor control (TIM2)

---

## System Operation

The system operates according to the following logic:

1. The **outside PIR sensor** detects a cat approaching the litter box.
2. The **inside PIR sensor** confirms the cat has entered.
3. After the cat leaves the litter box, the controller starts the **cleaning cycle**.
4. The motor rotates the cleaning mechanism using the **L293D motor driver**.
5. When the **180° limit switch** is triggered, the direction changes.
6. When the **0° limit switch** is reached, the motor stops and the system returns to standby.

If the cat re-enters the litter box during the cleaning cycle:

- the **PIR interrupt immediately stops the motor**
- the cleaning cycle resumes only after the cat leaves.

The system can also transmit status messages via **Bluetooth Low Energy using the HM-10 BLE module**.

---

## Software Architecture

The firmware is implemented using a **finite state machine**.

States used in the program:

CHECK_OUTSIDE
CHECK_INSIDE
VERIFY_OUTSIDE
MOVE_LEFT
MOVE_RIGHT
STOP_POSITION

Each state represents a stage of the cleaning process and ensures predictable system behavior.

---

## Features

- Event-driven system using **external interrupts**
- **PWM motor control**
- **L293D H-bridge motor driver**
- Safety stop when cat is detected during cleaning
- **Limit switch based position control**
- **Bluetooth communication (HM-10 BLE)**
- **UART communication**
- **Finite state machine control**

---

## Development Environment

The project was developed using:

- **STM32CubeIDE**
- **STM32 HAL drivers**
- **C programming language**

---

## ⚠ Safety Warning

This project is a **prototype and demonstration system**.

The current implementation relies mainly on **PIR motion sensors** to detect the presence of the cat inside the litter box.  
However, PIR sensors alone are **not a reliable safety mechanism**.

For a real-world automatic litter box system it is **strongly recommended to add a load cell (strain gauge weight sensor)** under the litter box.

Using a load cell allows the system to:

- reliably detect whether the cat is inside the litter box
- prevent the cleaning mechanism from starting while the cat is inside
- significantly improve system safety

Without a **load cell (tensometer)** the system **should not be considered safe for real-world use**.

---

## Possible Improvements

Future improvements may include:

- integration of a **load cell with HX711 amplifier**
- mobile application for **BLE communication**
- motor current monitoring
- automatic fault detection
- low-power standby mode
- improved safety logic

---

## Project Purpose

This project was created as a **practical embedded systems and electronics project** demonstrating:

- STM32 microcontroller programming
- sensor integration
- motor control
- Bluetooth communication
- real-time event handling
- embedded system architecture


