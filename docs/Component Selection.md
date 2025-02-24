---
title: Component Selection
---
  
### **Microcontroller**

| Solution | Pros | Cons |
|----------|----------|----------|
| pic cost | - Faster Processing for complex tasks<br>- Built in Wifi and Bluetooth 5 Connectivity<br>- Larger memory storage | - Higher Power Consumption<br>- Complex Peripheral Management<br>- Much more complex memory management |
| Pic cost | - Simple and easy architecture to program<br>- Multiple low power modes; overall low energy consumption<br>- More Reliable for wired standalone subsystems | - No built in wireless capabilities<br>- Fewer advanced I/O options<br>- Limited memory for advanced applications |
| Pic cost | - Faster Processing speed<br>- Adjustable GPIO pins<br>- 2 UART and 2 ICSP Pins | - Slower processing speeds<br>- No built in wifi or bluetooth modules<br>- Requires complex PCB design for high frequency operation |

**Choice:**  
Solution 2 - PIC18F47Q10T-I/PT

**Rationale:**  
The PIC18F47Q10T-I/PTc offers an excellent balance of versatility, functionality, and efficient use of board space. With a rich array of bidirectional I/O pins that support both digital and analog functions, along with configurable peripherals such as timers, communication interfaces, and the Peripheral Pin Select (PPS) feature, this module provides the flexibility needed to handle complex tasks and interface with various sensors and actuators. Additionally, the integration of low-power features and dedicated programming interfaces makes it ideal for projects requiring robust performance in energy-sensitive environments. This combination of features in a compact package ensures that the design is both scalable and cost-effective, meeting the project's performance and connectivity requirements without unnecessary complexity.


### **Voltage Regulator**

| Solution | Pros | Cons |
|----------|----------|----------|
| Pic cost | - High Efficiency<br>- High heat protection<br>- Prior use in class with through hole version | - Switch frequency make noise<br>- Limited Stock |
| Pic cost | - High Efficiency<br>- High Temperature Range | - Switch frequency make noise<br>- Low dropout Voltage<br>- 5.5 V Max Input |
| Pic cost | - High Efficiency<br>- Very Inexpensive | - Very Difficult Soldering<br>- Low max Temp<br>- 6.5 V Max Input |

**Choice:**  
Solution 1 - LM2575WU 

**Rationale:**  
The LM2575WU was chosen as our voltage regulator due to its efficiency, reliability, and ease of integration in our power management system. As a step-down (buck) switching regulator, it efficiently converts higher input voltages, such as 9V, to a stable 3.3V output, ensuring optimal power delivery while minimizing heat dissipation compared to traditional linear regulators. With a wide input voltage range (4V to 40V) and a 1A output current capacity, it provides flexibility for various power sources and load conditions. Its internal frequency compensation, fixed 52kHz switching frequency, and minimal external component requirements simplify circuit design and reduce PCB space. Additionally, the integrated thermal shutdown and current limit protection enhance system safety and durability. Given our prior experience and familiarity with this regulator, its selection ensures a seamless and efficient voltage regulation solution for our project.


### **Human Machine Interface (HMI)**

| Solution | Pros | Cons |
|----------|----------|----------|
| Pic cost | - Open Source Graphics library<br>- Peripheral rich (works with SPI, I2C, Arduino)<br>- Only needs 5V DC | - Most Expensive option<br>- Only 2.4 Inches in size |
| Pic cost | - Simple pin structure<br>- Only needs 3.3V<br>- Have prior knowledge of how to use | - Has a slower processing speed<br>- Only 0.96 in. in size |
| Pic cost | - Runs I2C and SPI<br>- Simple pin structure<br>- Relatively Inexpensive | - Only runs characters<br>- Has no backlight |

**Choice:**  
Solution 2 - Songhe 128x64 OLED Display

**Rationale:**  
The Songhe OLED display was chosen for this project due to its high contrast, and ultra-low power consumption (0.06W), making it ideal for clear and efficient data visualization. Its I²C communication simplifies interfacing with microcontrollers, reducing wiring complexity, while the wide 3.3V-5V power range ensures flexibility. The self-luminous OLED technology eliminates the need for a backlight, improving readability and durability in various lighting conditions. Additionally, our prior experience with this display in class allows for seamless integration, minimizing troubleshooting time.



