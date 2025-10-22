# 🔐 Secure Relay Lock System – STM32 (Assignment 3)

## 📘 Overview
This project implements a **time-restricted access control system** using an STM32 microcontroller.  
The relay lock opens only within authorized daily time windows and automatically re-locks after 8 seconds.  
It demonstrates **RTC alarm scheduling**, **interrupt-driven control**, and **finite-state machine (FSM)** logic with full safety handling.

---

## 🎯 Objectives
- Apply **RTC alarms** to enforce real-time control.  
- Implement **secure state transitions** that never leave the relay unintentionally ON.  
- Use **EXTI interrupts** for buttons with software debounce.  
- Provide **visual feedback** through two LEDs indicating current system state.  
- Check **RTC validity** on startup via backup register.

---

## ⚙️ Hardware Setup

| Component | Function | STM32 Pin |
|------------|-----------|-----------|
| Relay (Door Lock) | Activates 8 s on valid access | `PA0` |
| Green LED | Normal / door status | `PA1` |
| Red LED | Error / disabled indicator | `PA2` |
| Request Button | Access request input | `PB0` → EXTI0 |
| Supervisor Button | Enable / disable system | `PB1` → EXTI1 |
| RTC Crystal | Precise timekeeping source | LSE 32.768 kHz |

---

## 🧠 Functional Description
1. **Startup Check**  
   - Reads backup register (e.g. `0x32F2`) to verify RTC validity.  
   - If invalid → enters *RTC Error* mode (red LED blinks).

2. **Normal Operation**  
   - System runs only when **Supervisor = Enabled** and **RTC valid**.  
   - Two authorized windows: **07:45–12:00** and **13:00–17:30**.  
   - Outside window → idle (green LED 1 Hz blink).  
   - Inside window → ready (green LED 2 Hz blink).

3. **Access Request**  
   - Pressing the request button during a valid window unlocks the door for 8 s.  
   - Re-pressing within 8 s restarts the timer.  
   - On timeout (RTC Alarm A) → relay OFF automatically.

4. **Supervisor Mode**  
   - Toggles system enable/disable.  
   - Disabled → red LED ON, all requests ignored, relay forced OFF.

5. **Fail-Safe Behavior**  
   - Every state change ensures relay OFF first.  
   - Software debounce ≈ 100 ms prevents false triggering.

---

## 🧩 LED Patterns

| System State | Green LED | Red LED | Description |
|--------------|------------|----------|--------------|
| RTC Invalid | OFF | Blink (300/700 ms) | RTC not set |
| Disabled | OFF | ON | Supervisor OFF |
| Idle (Outside Window) | Blink 1 Hz | OFF | Waiting |
| Ready (Inside Window) | Blink 2 Hz | OFF | Accepting requests |
| Door Open | ON | OFF | Relay active |

---

## 💡 Key Code Highlights

### Check Authorized Windows
```c
uint8_t IsInWindow(uint8_t h, uint8_t m) {
  uint16_t mm = h * 60 + m;
  return ((mm >= 465 && mm < 720) || (mm >= 780 && mm < 1050));
}

```
