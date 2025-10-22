#  Three-Level Lighting System – STM32 (Assignment 4)

##  Overview
This project implements a **three-level lighting controller** with both **Manual** and **AUTO** modes on an STM32 microcontroller.  
Outputs `PA0`, `PA1`, `PA2` encode brightness levels. A **mode button** (EXTI) cycles through manual modes and AUTO.  
AUTO mode derives the level from **RTC time**. If RTC is not valid at boot, the system enters **ERROR** (red LED blink) until time is set.

---

##  Objectives
- Practice **RTC-based logic** and **interrupt-driven control**.
- Implement a **mode state machine** with immediate output updates.
- Provide **error handling** for invalid RTC and clear **visual feedback** via LEDs.
- Keep the firmware **non-blocking** and power-aware.

---

## ⚙️ Hardware Setup

| Component | Function | STM32 Pin (default) |
|----------|----------|---------------------|
| L0 (Level bit 0) | Brightness output | `PA0` |
| L1 (Level bit 1) | Brightness output | `PA1` |
| L2 (Level bit 2) | Brightness output | `PA2` |
| AUTO LED (Green) | ON in AUTO mode | `PA3` |
| ERROR LED (Red) | Blink if RTC invalid | `PA4` |
| Mode Button | Cycle Off→Low→Med→High→Auto | `PC13` → EXTI13 |
| RTC | Time source for AUTO | LSE 32.768 kHz (preferred) |

> You can remap pins to match your board; just update the pin macros in code.

---

## 🧠 Modes & Behavior

### Manual Levels (bit-encoding on PA2..PA0)
- **OFF**  → `000` (all OFF)  
- **LOW**  → `001` (PA0 ON)  
- **MED**  → `011` (PA0+PA1 ON)  
- **HIGH** → `111` (PA0+PA1+PA2 ON)

### AUTO Schedule (based on RTC time)
- **06:00–17:00** → **HIGH**  
- **17:00–23:00** → **MEDIUM**  
- **23:00–06:00** → **LOW**

### Mode Button (PC13, EXTI13)
Manual cycle: **Off → Low → Med → High → Auto → Off → …**  
In **AUTO**, time changes immediately update the level.  
If **RTC invalid**, system is locked in **ERROR**: requests ignored until RTC gets valid.

---

## Indicators
- **AUTO LED (Green / PA3):** ON in AUTO, OFF otherwise.  
- **ERROR LED (Red / PA4):** Blinks **300 ms ON / 700 ms OFF** when RTC is invalid.  

---

##  Firmware Structure
- **main.c** – Mode FSM, RTC checks, LED logic, EXTI handling.  
- **MX_RTC_Init / MX_GPIO_Init / SystemClock_Config** – generated via STM32CubeMX.  
- **RTC validity flag** – backup register (e.g., `BKP_DR1 = 0x32F2`) set once time is configured.

