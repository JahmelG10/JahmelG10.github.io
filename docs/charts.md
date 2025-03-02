---
title: Charts
---
## HMI Interface Block Diagram 

![3144BlockDiagram](https://github.com/JahmelG10/JahmelG10.github.io/blob/main/3144BlockDiagram.drawio.png?raw=true)---

## Power Budget


### Component Power Consumption

| **Component**            | **Voltage (V)** | **Current (mA)** | **Power (mW)** |
|-------------------------|-----------------|-----------------|-----------------|
| OLED Display           | **3.3V**        | **18mA**        | **59.4mW**      |
| PIC18F27Q10 MCU        | **3.3V**        | **10mA**        | **33mW**        |
| LM2575WU Quiescent      | **12V**         | **5mA**         | **60mW**        |
| Green LED              | **2V**          | **20mA**        | **40mW**        |
| Pull-up Resistors      | **3.3V**        | **3.62mA**      | **11.95mW**     |
| **Total Power Needed (3.3V Side)** | - | **51.62mA** | **144.35mW** |

---

### Voltage Regulator Efficiency

The **LM2575WU** operates with an efficiency of **~75%** at **12V input and 3.3V output**.

- **Power required at 3.3V side:** **144.35mW**
- **Power drawn from 12V source:**  
  \[
  {144.35mW}/{0.75} =approx 192.5mW
  \]
- **Current drawn from 12V source:**  
  \[
  {192.5mW}/{12V} =approx 16.04mA
  \]
- **Power dissipated as heat in regulator:**  
  \[
  192.5mW - 144.35mW = 48.15mW
  \]

---

### Final Power Summary

| **Power Rail** | **Current Draw (mA)** | **Power Dissipation (mW)** |
|---------------|-----------------|-----------------|
| **3.3V Load** | **51.62mA**     | **144.35mW**    |
| **12V Source** | **16.04mA**      | **192.5mW**     |
| **Regulator Heat Loss** | - | **48.15mW** |

---


This power budget helps in selecting the appropriate **power supply** and ensuring **thermal management** in the circuit.

