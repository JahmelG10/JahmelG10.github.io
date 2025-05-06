---
title: Board Design
---
**The schematic below details the Human Machine Interface (HMI) subsystem, ensuring fast real-time data display on the OLED screen from the sensor. This design incorporates several key sections, each serving a critical role in facilitating seamless data retrieval, processing, and visualization for the user.**

To support debugging and monitoring, the schematic includes a single debugging LED, providing a visual indicator for data transmission and system status. A reset button is integrated to facilitate system resets as needed. Additionally, dedicated headers are included to allow seamless connection with the Snap Debug Programmer, enabling efficient debugging and firmware updates.

A 3.3V voltage regulator is incorporated to ensure a stable power supply for the HMI subsystem. This schematic is designed to meet user needs and project requirements by enabling real-time data display, supporting UART communication, and facilitating efficient system debugging through dedicated interfaces.
## **Schematic**
[Download Schematic (PDF)](https://github.com/JahmelG10/JahmelG10.github.io/blob/main/Schematic_pdf2.pdf?raw=true)
![schemtic](https://github.com/user-attachments/assets/90dacd5c-1415-4509-939a-937d88ec0c50)








## **Download Links** 

- [Download Altium Project Workspace (ZIP)](https://github.com/JahmelG10/JahmelG10.github.io/blob/main/Project_Workspace.zip?raw=true)
- [Download Gerber Files (ZIP)](https://github.com/JahmelG10/JahmelG10.github.io/blob/main/Gerber.zip?raw=true)


## **PCB Design** 
[📄 Download PCB Layout (PDF)](https://github.com/JahmelG10/JahmelG10.github.io/blob/main/Binder1.pdf?raw=true)

### **Ecad Top Layer**
![PCB_front_cad](https://github.com/user-attachments/assets/5dfe5873-92c8-4408-9b2f-29b3bf347c17)

### **Ecad Bottom Layer**
![PCB_back_cad](https://github.com/user-attachments/assets/b8a9b6af-1d1e-4c64-969b-119708c11da2)

### **Manufacture Top Layer**
![pcbnaked](https://github.com/user-attachments/assets/8e47b74b-3fcb-4d15-a99c-5b64cda9fdae)

### **Manufacture Bottom Layer**

![pcbnakedback](https://github.com/user-attachments/assets/f8df26bd-ba47-4b5c-ad32-f2e941c8630f)

## **Bill of Materials**

![Bill of materials](https://github.com/user-attachments/assets/086d2c85-5e1f-4a61-8779-47f1a1fbcb01)
[Download Bill of Materials (Excel)](https://github.com/JahmelG10/JahmelG10.github.io/blob/main/website%20bill%20of%20materials.xlsx?raw=true)

## **Final Integrated and Soldered Team PCB**
### **Top Layer**
![Board_pcbfront](https://github.com/user-attachments/assets/ab2c3441-4981-4e04-a65f-82ff80a9460c)
### **Bottom Layer**
![Board_pcbback](https://github.com/user-attachments/assets/8ffdd10d-bf2e-4d37-a18c-10bf7b0a03c1)



### Functional Discussion: How the Schematic Meets Product Requirements

This schematic satisfies the project’s product and user requirements through clear functional design focused on usability, expandability, and system interaction:

- **OLED Display Integration**: The schematic includes header pins for the OLED display as provided in class. This enables flexible mounting—either on-board for compact integration or off-board for panel-mount applications—making the design adaptable to user needs and physical constraints.

- **Pushbutton Input Configuration**: It features two pushbuttons wired to GPIO pins configured as inputs. Each button is pulled up using a 10kΩ resistor and tied to ground on the opposite end, ensuring the microcontroller reads a logic high (`1`) by default and a logic low (`0`) upon press. This configuration supports interrupt-on-negative-edge detection, which is both efficient and reliable for HMI tasks.

- **Human-Machine Interface (HMI)**: Together, the OLED display and pushbutton inputs fulfill the requirements for a basic **HMI system**. Users can both view system information and interact with it, such as toggling modes or adjusting values, directly through hardware feedback and input.

This combination of visibility, input responsiveness, and flexibility directly addresses user interaction needs and adheres to core design requirements for embedded system interfaces.

### **Team Design and Decision-Making Process**

Originally, our team's design intended for the HMI PCB to be mounted at an angle outside of an enclosure that contained the other subsystems. This orientation allowed users to easily view the OLED display while also enabling accessible interaction with the onboard pushbuttons. The angled design was chosen to improve user ergonomics and maintain a compact layout by keeping the display and controls integrated on a single board.

As the project evolved, the team decided to shift to a more open presentation format. Instead of enclosing the subsystems, we made all boards visible and accessible to viewers, which supported better public engagement during demonstrations. The only components mounted externally on 3D-printed blocks were the temperature sensor and the heat lamp, which were positioned for functional interaction while maintaining visual clarity.

This decision allowed for improved visibility, easier debugging, and a more interactive user experience during our final presentation.


### **If I were to make a Version 2.0** 

If I were to create a Version 2.0 of my hardware design, one of the first major changes I would make is switching from the PIC18F27Q10 microcontroller to the ESP32. This change would greatly improve the development workflow and compatibility with peripheral components like the SSD1306 OLED display. The ESP32 has extensive community support and readily available libraries, particularly for I²C OLED displays, making the software side of integration much easier. In addition, the ESP32 includes clearly documented boot and reset circuitry, which is essential for stable programming. These features would not only make the board easier to develop with, but also more accessible for future users who want to expand on the design.
Another improvement would be to use larger, more ergonomic pushbuttons. The small tactile switches currently used are difficult to press and don’t stand out visually. Larger buttons would improve the user experience by providing better feedback and making the interface more obvious and inviting, especially in a demo setting where ease of interaction is critical.
One of the biggest lessons I learned from the current board was the importance of efficient power distribution. In the original layout, I relied on routing individual 3.3V traces across the board without dedicating a power plane. This created a cluttered layout and forced me to place multiple vias to connect power between layers. If I had implemented a dedicated top-layer power plane, I could have distributed power more cleanly and avoided long traces, improving electrical performance and simplifying the layout. In Version 2.0, this would be a priority to support better voltage stability and reduce electromagnetic interference.
Additionally, I would focus on reducing the overall size of the PCB. The current design is functional but bulkier than necessary, which made it harder to mount or enclose cleanly. A more compact layout, with tightly placed components and smarter routing, would result in a sleeker and more professional product.
Finally, I would replace the adjustable voltage regulator with a fixed 3.3V regulator. Since my system only uses a 12V input and 3.3V output, the adjustable regulator—while functional—required two external resistors to set the output voltage. A fixed regulator would eliminate this need, saving space, reducing component count, and simplifying soldering. It would also be slightly cheaper, making the design more efficient in both cost and labor. These changes, grounded in what I learned from the schematic and build process, would make Version 2.0 a cleaner, more robust, and more user-friendly design.




























