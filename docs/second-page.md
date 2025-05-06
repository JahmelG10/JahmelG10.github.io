---
title: Board Design
---
**The schematic below details the Human Machine Interface (HMI) subsystem, ensuring fast real-time data display on the OLED screen from the sensor. This design incorporates several key sections, each serving a critical role in facilitating seamless data retrieval, processing, and visualization for the user.**

To support debugging and monitoring, the schematic includes a single debugging LED, providing a visual indicator for data transmission and system status. A reset button is integrated to facilitate system resets as needed. Additionally, dedicated headers are included to allow seamless connection with the Snap Debug Programmer, enabling efficient debugging and firmware updates.

A 3.3V voltage regulator is incorporated to ensure a stable power supply for the HMI subsystem. This schematic is designed to meet user needs and project requirements by enabling real-time data display, supporting UART communication, and facilitating efficient system debugging through dedicated interfaces.
## **Schematic**
![schemtic](https://github.com/user-attachments/assets/90dacd5c-1415-4509-939a-937d88ec0c50)








## **Download Links** 
- [Download Schematic (PDF)](https://github.com/JahmelG10/JahmelG10.github.io/blob/main/Schematic_pdf2.pdf?raw=true)
- [Download Altium Project Workspace (ZIP)](https://github.com/JahmelG10/JahmelG10.github.io/blob/main/Project_Workspace.zip?raw=true)
- [Download Gerber Files (ZIP)](https://github.com/JahmelG10/JahmelG10.github.io/blob/main/Gerber.zip?raw=true)


## **PCB Design** 
### **Ecad Top Layer**
![PCB_front_cad](https://github.com/user-attachments/assets/5dfe5873-92c8-4408-9b2f-29b3bf347c17)

### **Ecad Bottom Layer**
![PCB_back_cad](https://github.com/user-attachments/assets/b8a9b6af-1d1e-4c64-969b-119708c11da2)

### **Manufacture Top Layer**
![pcbnaked](https://github.com/user-attachments/assets/8e47b74b-3fcb-4d15-a99c-5b64cda9fdae)

### **Manufacture Bottom Layer**

![pcbnakedback](https://github.com/user-attachments/assets/f8df26bd-ba47-4b5c-ad32-f2e941c8630f)

## **Final Integrated and Soldered Team PCB**
### **Top Layer**
![Board_pcbfront](https://github.com/user-attachments/assets/ab2c3441-4981-4e04-a65f-82ff80a9460c)
### **Bottom Layer
![Board_pcbback](https://github.com/user-attachments/assets/8ffdd10d-bf2e-4d37-a18c-10bf7b0a03c1)

## **Bill of Materials**

![Bill of materials](https://github.com/user-attachments/assets/086d2c85-5e1f-4a61-8779-47f1a1fbcb01)
[Download Bill of Materials (Excel)](https://github.com/JahmelG10/JahmelG10.github.io/blob/main/website%20bill%20of%20materials.xlsx?raw=true)

### Functional Discussion: How the Schematic Meets Product Requirements

This schematic satisfies the project’s product and user requirements through clear functional design focused on usability, expandability, and system interaction:

- **OLED Display Integration**: The schematic includes header pins for the OLED display as provided in class. This enables flexible mounting—either on-board for compact integration or off-board for panel-mount applications—making the design adaptable to user needs and physical constraints.

- **Pushbutton Input Configuration**: It features two pushbuttons wired to GPIO pins configured as inputs. Each button is pulled up using a 10kΩ resistor and tied to ground on the opposite end, ensuring the microcontroller reads a logic high (`1`) by default and a logic low (`0`) upon press. This configuration supports interrupt-on-negative-edge detection, which is both efficient and reliable for HMI tasks.

- **Human-Machine Interface (HMI)**: Together, the OLED display and pushbutton inputs fulfill the requirements for a basic **HMI system**. Users can both view system information and interact with it, such as toggling modes or adjusting values, directly through hardware feedback and input.

This combination of visibility, input responsiveness, and flexibility directly addresses user interaction needs and adheres to core design requirements for embedded system interfaces.































