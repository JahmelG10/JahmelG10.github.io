---
title: Block Diagram
---
## HMI Interface Block Diagram
---
[Download HMI Block Diagram (PDF)](https://github.com/JahmelG10/JahmelG10.github.io/blob/main/314HMI.drawio.pdf?raw=true)


![314HMI](https://github.com/user-attachments/assets/d0099a2c-6e9a-4c51-9dbf-18a4bac1677b)






### **Decision-Making Process and Block Diagram Justification** 
I developed my block diagram by identifying and organizing all critical components and connections required for the functionality of my board. My goal was to clearly represent the system architecture, data flow, and how each subsystem interfaces with the microcontroller.
The block diagram meets the project requirements by illustrating the following:
UART Communication: It includes two UART header blocks that clearly indicate the direction of RX and TX lines for both upstream and downstream communication.


I²C Interface: It shows the OLED display connected to the microcontroller via the SDA and SCL lines, fulfilling the display integration requirement.


GPIO Inputs: Push buttons are connected to specific GPIO pins, with labeled functionality, demonstrating user input integration.


Power Regulation: The diagram includes a switching regulator powered through a barrel jack connected to an external wall outlet, which satisfies the off-board power supply requirement.


This layout ensures that all major subsystems are accounted for and that their communication and power pathways are transparent and logically organized to meet both functional and project constraints.




