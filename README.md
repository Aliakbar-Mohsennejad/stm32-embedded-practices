#  STM32 Microcontroller Coursework Repository

##  Overview
This repository contains a complete collection of academic assignments for the **Microprocessor Systems** course, designed around practical applications of **STM32 microcontrollers**. Each project explores hardware control, RTC time management, low-power modes, and clock configuration using the STM32 HAL library.

---

##  Academic Context
**Course:** Microprocessor Systems  
**Instructor:** Dr. Rouhollah Yarmand  
**Teaching Assistant (TA):** Ali Akbar Mohsennjad  
**Faculty:** Electrical and Computer Engineering  
**Semester:** Fall 2025

---

##  Assignments Overview

###  Clock Management in STM32
This assignment covers the internal and external clock management systems in STM32 microcontrollers, including:
- HSI, HSE, LSI, LSE, and PLL clock sources
- The use of the Clock Security System (CSS)
- Configuration of AHB and APB bus systems

**Goal:** Understand how clock sources affect timing, power, and performance in embedded systems.

---

###  Smart Irrigation System
An **RTC-based automated irrigation controller** that activates a water valve twice daily (at 9:00 AM and 9:00 PM) for exactly 10 minutes.  
- Relay controlled through **PA0**
- EXTI button toggles enable/disable state
- RTC keeps precise timing
- Designed for minimal power consumption

**Features:**
- RTC alarms for scheduling
- Debounced EXTI interrupt for user control
- Safe shutdown and enable logic

---

###  Secure Relay Lock System
A **time-window–restricted access controller** for a relay-based lock.  
The lock accepts access requests only between **07:45–12:00** and **13:00–17:30**.

**Key Functionalities:**
- 8-second timed unlock via RTC Alarm A
- Pressing the button again restarts the timer
- Supervisor button disables the system
- RTC validation check at startup
- Dual LEDs (green and red) indicate system state

**Fail-Safe Design:**
- Relay always OFF at startup or mode transitions  
- Button bounce filtered using software debounce

---

###  Three-Level Lighting System
Implements a **multi-level lighting controller** with both **manual** and **AUTO** modes.

**Outputs:** `PA0`, `PA1`, `PA2`  
**Mode Logic:**
- High: All ON (06:00–17:00)  
- Medium: Two ON (17:00–23:00)  
- Low: One ON (23:00–06:00)  
- Off: All OFF  
- AUTO: Automatically adjusts based on RTC time

**Additional Features:**
- Mode selection via button on `PC13` (EXTI13)
- Green LED indicates AUTO mode
- Red LED blinks when RTC invalid (300ms ON / 700ms OFF)
- Immediate correction when RTC time changes

---

###  Power Modes and Clock Sources
An analytical and practical comparison between **STM32F1** and **STM32L4** families in terms of:
- Power modes: Run, Sleep, Stop, and Standby
- Clock sources: HSE, HSI, MSI, LSE, LSI, PLL
- Energy optimization techniques

**Power Optimization Techniques:**
- Use of LSE for accurate RTC timekeeping
- Peripheral clock gating via RCC
- GPIO configuration to prevent floating inputs
- DMA and peripheral autonomy (Timer → ADC → DMA → RAM)

**Outcome:** Achieve maximum energy efficiency and system reliability for embedded and IoT applications.

---

##  Technical Information
- **Language:** C (HAL Library)
- **IDE:** STM32CubeIDE / STM32CubeMX
- **Microcontroller:** STM32F103C8T6 or STM32L4 series
- **Peripherals Used:** GPIO, RCC, RTC, EXTI, DMA, NVIC
- **Power Modes:** Sleep / Stop / Standby with RTC backup

---

##  Learning Outcomes
- Configuration of STM32 clocks and buses (RCC, PLL, HSE, LSE).  
- Development of RTC-based time management systems.  
- Implementation of interrupt-driven control (EXTI).  
- Design of low-power embedded systems.  
- Use of DMA and peripheral triggers for energy saving.

---

## 📁 Repository Structure
```
STM32_Coursework/
├── Assignment1_Clock_Management/
├── Assignment2_Smart_Irrigation/
├── Assignment3_Secure_Relay_Lock/
├── Assignment4_Lighting_System/
├── Assignment5_Power_Modes/

```

---

##  Tools & Frameworks
- **STM32CubeIDE / STM32CubeMX** – Configuration and firmware generation  
- **HAL Library** – Hardware Abstraction Layer by STMicroelectronics  
- **CMSIS** – ARM Cortex core interface standard  
- **ST-Link / OpenOCD** – Flashing and debugging tools  

---

##  Author Information
**Teaching Assistant:** Ali Akbar Mohsennjad  
**Instructor:** Dr. Rouhollah Yarmand  
📧 Email: [pooyamohsennjad@gmail.com](mailto:pooyamohsennjad@gmail.com)  
🔗 LinkedIn: [linkedin.com/in/ali-akbar-mohsennjad](https://linkedin.com/in/ali-akbar-mohsennjad)

---

## 📄 License
This repository is for **educational and academic use only**.  
© 2025 Ali Akbar Mohsennjad & Dr. Rouhollah Yarmand – All Rights Reserved.
