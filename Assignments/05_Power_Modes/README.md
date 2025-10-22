#  STM32 Power Modes and Clock Sources (Assignment 5)

##  Overview
This assignment explores **power management and clock architecture** in STM32 microcontrollers, comparing a general-purpose family (**STM32F1**) with an ultra-low-power family (**STM32L4**).  
It explains how power modes, clock sources, and peripheral configurations affect **energy efficiency**, **system performance**, and **timing precision**.  
Finally, it covers **DMA and autonomous peripherals** as techniques to reduce CPU activity and extend battery life.

---

##  Objectives
- Understand and compare **power modes** in STM32F1 vs STM32L4.  
- Learn about different **clock sources** and their trade-offs.  
- Explore methods for **low-power operation** using RTC and LSE.  
- Apply **RCC clock gating**, **GPIO optimization**, and **DMA-based autonomy** to reduce energy consumption.

---

##  1. Power Modes in STM32

### STM32F1 Family (General Purpose)
| Mode | Description | Wake-up | Power |
|------|--------------|----------|--------|
| **Run** | CPU and all peripherals active | Immediate | High |
| **Sleep** | CPU halted, peripherals running | Interrupt | Medium |
| **Stop** | Most clocks off, RAM retained | EXTI / RTC | Low |
| **Standby** | Only RTC domain active, RAM lost | Wake-up pin / Reset | Ultra Low |

### STM32L4 Family (Ultra-Low-Power)
| Mode | Description | Notes |
|------|--------------|-------|
| **Run** | Frequency and voltage scaling for performance control | Dynamic power saving |
| **Low-Power Sleep** | CPU halted, selected peripherals active | Similar to Sleep |
| **Stop 0 / Stop 1 / Stop 2** | Progressive shutdown of clocks/regulators | Retains RAM, microamp currents |
| **Standby / Shutdown** | All logic off except RTC and optional backup RAM | Ideal for long battery life |

 Compared to STM32F1, STM32L4 provides **finer control** over regulator and oscillator domains and can operate in the **microamp range**.

---

##  2. Clock Sources Overview

| Source | Type | Accuracy | Power | Typical Use |
|---------|------|-----------|--------|--------------|
| **HSE** | External crystal/oscillator | Very high | High | Precise core clock |
| **HSI** | Internal RC (~8–16 MHz) | Medium | Moderate | Default boot clock |
| **MSI** | Multi-Speed Internal (100 kHz–4 MHz) | Medium | Very Low | Low-power operation |
| **LSE** | 32.768 kHz external crystal | Very high | Very Low | RTC & timekeeping |
| **LSI** | Internal ~37 kHz RC | Low | Minimal | Watchdog or backup |
| **PLL** | Frequency multiplier | Very high | High | Performance boost |

---

## 3. Combining Clocks for Low-Power Operation
For long idle or battery-powered systems:

- Use **LSE** to keep **RTC** running accurately.  
- Use **MSI** or **HSI** for quick wake-ups.  
- Activate **PLL** only during high-performance tasks.  

This combination ensures both **precision** and **low power**.

---
