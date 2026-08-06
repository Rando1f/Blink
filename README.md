# Blink
Blink is a desk tracking device that tracks the user's time spent on the desk per session, displaying different animations based on how long the user has been going for. It uses an ultrasonic sensor that measures the distance between the user and itself. If that distance was lower than 15 in., it tracks that the user has been sitting on his desk. If it is more than 15 in., it tracks that the user is away from his desk. 
the animation are vresions of the same mascot "rando1f"<p align="right"><img src="assests/Journal assests/Idle animation.gif"></p>

### Used appication
multiple applications were used in the creatino of blink starting with 
<ul>
    <li>piskel: for animated pixelated gifs</li>
    <li>wokwi: for basic connection simulations</li>
    <li>Kicad: for PCB creation</li>
    <li>Auto desk fusion360: for the case creation</li>
    <li>VS code: for writing code and uploading it to the esp32   *must be paired with platformio extension</li>
</ul>

### How to use blink
Blink's code is meant to be flashed into an ESP32. This could be done through buying the PCP that was published in [production](production) here through the Gerber files, or through using a breadboard with the following wiring.This is going to be done through VS Code and PlatformIO or Arduino IDE, although I recommend using Visual Studio Code because it offers an easier time debugging or adding features if you want to.  
<p align="center"><img src="assests/Journal assests/final breadboard wiring.png" width="500"></p>

blink is plugged into the users device through a micro-usb port that has clearance of about 0.5 mm in the case and is mounted on the bottom of your desk after you screw the lid with body of the case either through superglue or a doubled face tape since blink is fairly light.


### pcb 
BLINK PCB is built on the wiring showcased in the How to use BLINK section, where it links all of the components to an NGND with an OLED screen having a 3.3 V input with normal I2C protocol wiring, which is SDA: pin 21 and SCL: pin 22.
on the other hand HC-SR04 Has a VIN or a 5V input, and due to the ESP32's 3.3V capacity, a voltage divider of two resistors: Resistor 1 being 220, Resistor 2 being 330, To bring the voltage down towards the 3V, so it doesn't fry or break the ESP32 with default wiring of trig: pin 5 and echo: pin 18.  
the esp32 used in this project was esp32 devkit 30pin.
the dimensions of the pcb are: 74.93*85.55*20

<table>
<tr>
    <td width="50%"><img src="assests/PCB images/pcb electronic symbol.png" width="550">
<img src="assests/PCB images/pcb footprint.png" width="550">.</td>
    <td width="50%"> <img src="assests\PCB images\3d viewer.png"></td>
</tr>
</table>

### Case
the case was done with rough parts mesurments (beside the pcb with a 0.2mm tolarnce) and a casse thickness of 10mm.
the case features an ultrasonic sensor opening and an oled screen display cut extrusion where the oled screen would lie on a 90 degree angle with it being connecetd to the pcb trough jumper wires.
there are 4 studs on the 4 corners on the inside of the case to have a 3mm clearance below for all of the conections.
the case dimensions: 95.13mm *105.75mm *35 mm
the oled display dimensions: 20 mm* 27 mm
hc-sro4 diameter: 20
<p align="center"><img src="assests/CAD  images/cover 3-4 view.png" width="400"><img src="assests\CAD  images\noncover view.png" width="415"></p>


#### AI use

AI was only used for research purposes, and it wasn't used excessively. Rather, it was used as a resource-gathering tool so I could understand more of the project. The read.me is fully human-written, as well as the journal and the bill of materials. 
