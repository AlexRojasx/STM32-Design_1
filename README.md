# STM32-Design_1

<h2>Project Description:</h2>

The STM32 Design project's primary focus is to provide experiance working with the STM microcontroller and microcontrollers in general. The board utilizes an external clock, bypass capacitors, analog filtering,
and a mirco Usb port for power and coding. Also the Board includes the SWD pins for debugig, as well as UART and I2C capabilities. This project was used to deepen my understanding of various aspects of PCB design and microcontroller implementation.

<h2>Skills Learned:</h2>

- PCB Design and Layout  
- Microcontroller implementation and Noise Filtering
- External Cystal Oscillator implementation
- Stitching Vias
- Proper Grouding
- Mounting Holes
- Proper Schematic Layout

<h2>Tools Used:</h2> 

- Kicad for PCB Layout and Design  
- STM 32 Cube IDE

<h2>Screenshots:</h2>

Decoupling and power of the STM32F103C8T6:

![image](https://github.com/user-attachments/assets/b6ba5c25-0568-4660-bd1c-f61420159d29)

For every VDD pin, I placed a corresponding 100nF capacitor for noise filtering as well as including a 10uF for more filtering. For the VDDA pin, I utilized a ferrite bead and some more capacitors to filter out any digital noise from the Analog power.

NRST and BOOT0 circuits:

![image](https://github.com/user-attachments/assets/0f6e7045-8e04-4898-bade-2c14a34e6a34)

The NRST Pin is the reset pin with inverted logic, meaning the microcontroller will be put into reset mode when the pin is pulled low. The STM32 microcontrollers contain an internal pull-up resistor so the NRST pin can be left floating. I included a 100nF decoupling capacitor to prevent the pin from resetting from any noise or induced currents. The BOOT0 pin when pulled low will allow the microcontroller to run the program already flashed on it, so to program the microcontroller with USB, UART, or I2C, I've added a switch to pull the pin high when the user wants to reprogram the device.

Crystal Occilator and capacitor circuit:

![image](https://github.com/user-attachments/assets/5feb4eef-28c2-4db9-91da-38555a407610)

this part of the schematic details the external 16 MHz crystal oscillator and the external capacitors for proper operation of the crystal oscillator. The value was calculated by doubling the load capacitance of the crystal minus any stray capacitance which gave me around 10pF for this crystal oscillator.

USB Micro and SWDIO/SWCLK circuits:

![image](https://github.com/user-attachments/assets/149c4ce7-98bb-4ed6-9f72-2156b4a2e59e)

The power pins from the micro USB B are connected to ground and VBUS, which connects to the 5v-3.3v power regulator on the board. The differential pair is connected directly to the microcontroller with the D+ line connected to a pull-up resistor for the microcontroller to detect the USB as the correct version. The SWD pins are PA13 and PA14 on the microcontroller and connected to a 4-pin connector surrounded by 3.3v and ground for proper signal integrity.

Final Microcontroller (and USB) Schematic:

![image](https://github.com/user-attachments/assets/4f7a64b3-e1f5-4e96-9c5b-aa64fd3e29db)

The UART and I2C pins are connected to their own 4 pin connectors with pull up resistors on the I2C wires connected to 3.3v

Final Power supply Schematic:

![image](https://github.com/user-attachments/assets/16f954f1-5be2-4ce6-9033-75ad57f346de)

This 5v-3.3v power supply is similar to the 5v project I did with 22u decoupling capacitors to filter out any noise on both sides of the AMS1117 IC. I also included a red power indicating Led that runs at a few mA.

Rough PCB Layout:
![image](https://github.com/user-attachments/assets/adce45fc-2a3f-4d29-a405-fe53462fc709)

For the PCB layout, I started by making different groupings of parts, one group for the power supply, a group for the microcontroller and decoupling capacitors, a group for the pinouts like UART, I2C, SWD, and a group for the BOOT0 components. With each of the groupings made, I started organizing and placing the decoupling capacitors for the microcontroller, I placed them physically close to each of the VDD pins so the microcontroller gets as little noise as possible. I then moved on the placing the ferrite bead and the Crystal Oscillator next to the microcontroller. While placing and adjusting these components I tried to minimize the amount of crossed air wires to make my routing easier. After placing and adjusting the microcontroller components, I placed the USB and voltage regulator components, making sure that the noisy power supply was located farther from the sensitive components like the crystal oscillator or the 10uF capacitor for the microcontroller.

Final PCB Trace Routing:

![image](https://github.com/user-attachments/assets/a03c783e-feb1-4113-aec9-2c457bf69513)

Starting with the important signal wires first, I routed the crystal oscillator, the USB differential pairs, and the UART, SWD, I2C, and BOOT 0 pins with a 0.3 mm trace width. After routing the signal traces I routed any ground pads with a short 0.5mm wide trace connected to a via on the bottom ground plane. This allows for minimal ground traces on the top that might clutter up the board, and direct access to ground for all components, also using a ground plane on the bottom allows for less EMI between signal wires as the signal couples to the ground plane. After routing the ground, I moved on to routing power using a 0.5 mm wide trace and copper pours to connect the USB power to the power supply. The pours also included a ground pour near the power supply which I used stitching vias for effective grounding. While routing the power traces, I tried to minimize the amount of vias and traces on the bottom, especially under signal wires, to lessen any EMI interference. Also, wherever there were right angles I added a little bevel to allow for easier power transfer and 45-degree angles look nice. 

PCB 3d view: 

![image](https://github.com/user-attachments/assets/85a95ae5-f6e3-42f4-88ad-e3b444746fdd)

<h2>What Could be Improved:</h2>

Unfortunately, I am unable to physically build the PCB which would help with any debugging if there are any problems. Since the design and schematic are very similar to the video, I have a lot of the same parts and component placement as Phil's Lab. To Improve, I can create another microcontroller circuit with different pin configurations and components to get more practice creating microcontroller boards. 

<h2>Video i'm basing this project on:</h2>

https://www.youtube.com/watch?v=aVUqaB0IMh4

I am mainly using the schematic for the STM32 board, but designing the layout and component placement myself using the tips from the video to decide component placement.
