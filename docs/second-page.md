---
title: Board Design
---
**The schematic below details the Human Machine Interface (HMI) subsystem, ensuring fast real-time data display on the OLED screen from the sensor. This design incorporates several key sections, each serving a critical role in facilitating seamless data retrieval, processing, and visualization for the user.**

To support debugging and monitoring, the schematic includes a single debugging LED, providing a visual indicator for data transmission and system status. A reset button is integrated to facilitate system resets as needed. Additionally, dedicated headers are included to allow seamless connection with the Snap Debug Programmer, enabling efficient debugging and firmware updates.

A 3.3V voltage regulator is incorporated to ensure a stable power supply for the HMI subsystem. This schematic is designed to meet user needs and project requirements by enabling real-time data display, supporting UART communication, and facilitating efficient system debugging through dedicated interfaces.
## **Schematic**


![Block Diagram](https://github.com/JahmelG10/JahmelG10.github.io/blob/main/Schematic_pdf2.pdf)


## **Download Links** 
- [PDF](https://github.com/user-attachments/files/18934561/Individual_Subsytem_Schematic.1.pdf)
- [Cadence ZIP Folder](https://github.com/JahmelG10/JahmelG10.github.io/raw/refs/heads/main/EGR314_INDIVIDUAL_SCHEMATIC_0.zip)

## **PCB Design** 
coming soon


























## Power Budget





---

### All Major Components (Absolute Maximum Current Draw)

| **Component Name**        | **Part Number**       | **Supply** | **#** | **Absolute (mA)** | **Total (mA)** | **Unit** |
|-------------------------|----------------------|-----------|------|----------------|---------------|--------|
| **PIC18F27Q10 MCU**     | PIC18F27Q10-I/SO    | **+3.3V**     | 1    | **50**           | **50**         | **mA**     |
| **OLED Display**        | SSD1306               | **+3.3V**     | 1    | **25**           | **25**         | **mA**     |
| **Green LED**           | Generic LED (Green)   | **+3.3V**     | 1    | **20**           | **20**         | **mA**     |
| **Pull-up Resistors**   | 10kΩ & 4.7kΩ          | **+3.3V**     | 5    | **3.62**         | **3.62**       | **mA**     |

---

### +3.3V Power Rail (Absolute Maximum Current Draw)

| **Component Name**        | **Part Number**       | **Supply** | **#** | **Absolute (mA)** | **Total (mA)** | **Unit** |
|-------------------------|----------------------|-----------|------|----------------|---------------|--------|
| **PIC18F27Q10 MCU**     | PIC18F27Q10-I/SO    | **+3.3V**     | 1    | **50**           | **50**         | **mA**     |
| **OLED Display**        | SSD1306               | **+3.3V**     | 1    | **25**           | **25**         | **mA**     |
| **Green LED**           | Generic LED (Green)   | **+3.3V**     | 1    | **20**           | **20**         | **mA**     |
| **Pull-up Resistors**   | 10kΩ & 4.7kΩ          | **+3.3V**     | 5    | **3.62**         | **3.62**       | **mA**     |

- **Subtotal:** **98.62mA**  
- **Safety Margin (25%)**: **+24.66mA**  
- **Total Current Required on +3.3V Rail:** **123.28mA**  

---

### c4. Regulator or Source Choice (Absolute Maximum Ratings)

| **Regulator Name**     | **Supply Input** | **Output Voltage** | **Max Output Current** |
|----------------------|---------------|----------------|------------------|
| **LM2575WU (Buck Converter)** | **+12V**          | **+3.3V**          | **1A (1000mA)** |

- **Total Remaining Current Available on +3.3V Rail**: **876.72mA**  

---

### External Power Source 1 (Absolute Maximum Ratings)

| **Power Source**      | **Part Number**    | **Input** | **Output** | **Absolute Current** | **Total Current (mA)** |
|--------------------|-----------------|--------|--------|-----------------|----------------|
| **Power Source Selection** | Plug-in Wall Supply | **110V AC**  | **+12V DC** | **6000mA**          | **6000mA**         |
| **Power Rails Connected** | LM2575WU Regulator  | **+12V**     | **+3.3V**   | **1000mA**          | **1000mA**         |

- **Total Remaining Current Available on External Power Source 1**: **5000mA**  

---

### Key Adjustments:
- **PIC18F27Q10 Absolute Max Current:** Updated from **10mA** → **50mA**.
- **OLED Display Absolute Max Current:** Updated from **18mA** → **25mA**.
- **Total +3.3V Current Requirement Updated** to include **safety margin**.

This power budget accounts for absolute maximum current draws to ensure a robust and reliable power supply design.

