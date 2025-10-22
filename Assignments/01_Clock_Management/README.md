# 🧩 Assignment 01 – Clock Management in STM32 Microcontrollers

## 📘 Overview
This assignment focuses on understanding and configuring the **clock system (RCC)** in STM32 microcontrollers, especially in the STM32F1 family.  
It explores the internal and external clock sources, PLL configuration, clock security features, and bus structures (AHB & APB).  
The goal is to develop a solid understanding of how the system clock and peripheral clocks are generated, managed, and optimized for performance or low power.

---

## 🧠 Assignment Questions

### 1. Clock Management in STM32
Answer the following questions clearly and concisely:

**a)** What modes are available for configuring the internal clock in STM32 microcontrollers?  
Explain each mode briefly.

**b)** In STM32F1 series microcontrollers, how many input clock paths exist?  
Why has this number of paths been provided?

**c)** If we want the internal clock frequency of the microcontroller to be higher than the input frequency, which unit should be used?  
Explain how it works.

**d)** What is the purpose of the **Enable CSS** option in the clock configuration settings?

**e)** Research and explain briefly about the **AHB** and **APB** buses.  
What are their characteristics, and which peripherals typically use each of them?

---

## 🎯 Learning Objectives
By completing this assignment, you will:
- Understand the internal and external clock sources of STM32 (HSI, HSE, LSI, LSE, PLL).  
- Learn the purpose and configuration of the PLL unit for frequency multiplication.  
- Understand the role of the **Clock Security System (CSS)**.  
- Identify the structure and purpose of **AHB** and **APB** buses in distributing system clocks.  
- Build a foundation for precise timing and peripheral performance control in embedded systems.

---

## ⚙️ Recommended Tools
- **STM32CubeIDE** (for clock tree visualization and configuration)  
- **STM32CubeMX** (for generating initialization code)  
- Reference Manual: `RM0008` (STM32F1) – RCC Section  

---

## 🧾 Author
**Ali Akbar Mohsennjad**  
Embedded Systems Engineer | STM32 Developer  
📧 [Email](mailto:pooyamohsennjad@gmail.com)  
🔗 [LinkedIn](https://linkedin.com/in/ali-akbar-mohsennjad)

---


