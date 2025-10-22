#  Smart Irrigation System – STM32 (Assignment 2)

##  Overview
This assignment implements a **real-time automatic irrigation controller** using the **RTC (Real-Time Clock)** peripheral of an STM32 microcontroller.  
The system turns a water valve **ON** twice per day (at **09:00 AM** and **09:00 PM**) for exactly **10 minutes**, controlled through a relay on pin **PA0**.  
A **push-button input (EXTI0)** allows the user to enable / disable the entire irrigation logic at runtime.

---

##  Objectives
- Demonstrate use of **RTC timekeeping** and **alarm scheduling**.  
- Apply **GPIO** output control (relay → valve).  
- Handle **external interrupts (EXTI)** for user input with software debounce.  
- Implement **non-blocking timing** using RTC alarms rather than delay loops.  
- Combine **low-power standby capability** with accurate real-time control.

---

##  System Description
| Component | Function | STM32 Pin |
|------------|-----------|------------|
| Relay (Water Valve) | Turns irrigation ON/OFF | `PA0` (Output) |
| Control Button | Toggles system Enable/Disable | `EXTI0` (Input) |
| RTC | Provides current time & Alarm A events | Internal RTC (LSE preferred) |

### Operating Logic
1. When **enabled**, the program monitors RTC time.  
2. At 09:00 or 21:00 exactly, it activates the relay (valve ON).  
3. A **10-minute (600 s)** alarm is scheduled via RTC.  
4. When the 10 minutes elapse, an interrupt turns the relay OFF.  
5. If the user presses the EXTI button while irrigation is running, the system disables immediately and the relay is forced OFF.  
6. Upon re-enabling, the next valid alarm is re-scheduled.

---

## 🧩 Main Functional Blocks
- **RTC Alarm A** – used for both “start irrigation” and “stop after 10 min.”  
- **EXTI Interrupt** – toggles `system_enabled` flag; includes 100 ms debounce.  
- **GPIO Control** – drives the relay; default OFF at startup.  
- **State Machine**  
  - `ENABLED` / `DISABLED`  
  - `IRRIGATING` / `IDLE`  

---

##  Recommended Configuration
- **Clock Source:** LSE (32.768 kHz) for high-accuracy RTC  
- **RTC Format:** 24-hour  
- **Toolchain:** STM32CubeIDE + HAL Drivers  
- **Target Board Example:** STM32F103C8 or Nucleo-F103RB  

---

## 🧾 Example Code Summary
Key logic excerpt (see full `main.c`):
```c
// In HAL_RTC_AlarmAEventCallback():
if (g_next_action == ACT_START_IRR) {
    Relay_On();
    Schedule_Stop_After_10min();     // next alarm after 600s
}
else if (g_next_action == ACT_STOP_IRR) {
    Relay_Off();
    Schedule_Next_Start();           // set next 09:00 or 21:00
}
```


