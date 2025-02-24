---
title: Charts
---
## HMI Interface Block Diagram 

![314BlockDiagram](https://github.com/user-attachments/assets/ec5c0d30-a443-4bcc-9e63-ed41330f5141)---

## Power Budget

## Component Power Consumption Table

| **Component**            | **Voltage (V)** | **Current (mA)** | **Power (mW)** |
|-------------------------|-----------------|-----------------|-----------------|
| OLED Display           | **3.3V**        | **18mA**        | **59.4mW**      |
| PIC18F47Q10 MCU        | **3.3V**        | **10mA**        | **33mW**        |
| LM2575WU      | **9V**          | **5mA**         | **45mW**        |
| Pull-up Resistors      | **3.3V**        | **3.62mA**      | **11.95mW**     |
| **Total Power Needed (3.3V Side)** | - | **31.62mA** | **104.35mW** |

## Accounting for Voltage Regulator Efficiency

The **NCV2575** operates with an efficiency of **~77%** at **9V input and 3.3V output**.

- **Power required at 3.3V side:** **104.35mW**
- **Power drawn from 9V source:**  
  \[
  \{104.35mW}/{0.77} =approx 135.5mW
  \]
- **Current drawn from 9V source:**  
  \[
  \{135.5mW}/{9V} =approx 15.1mA
  \]
- **Power dissipated as heat in regulator:**  
  \[
  135.5mW - 104.35mW = 31.15mW
  \]

## Final Power Summary

| **Power Rail** | **Current Draw (mA)** | **Power Dissipation (mW)** |
|---------------|-----------------|-----------------|
| **3.3V Load** | **31.62mA**     | **104.35mW**    |
| **9V Source** | **15.1mA**      | **135.5mW**     |
| **Regulator Heat Loss** | - | **31.15mW** |

---

This power budget helps in selecting the appropriate **power supply** and ensuring **thermal management** in the circuit.

