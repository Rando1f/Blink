---
Title: BLINK
Author: Rando1f
Description: a desk companion montiring desk time with an artistic flair
Created_at: 27 / 7 / 2026
---
#### Total time spent: 45 hours
---
### Day 1 - getting started

Day one was primarily utilized through understanding the fundamentals of C and C++ Mainly void setup and void loop to understand how code is written and how I could write it in the future in order to use it properly, this was paired with acquiring knowledge about libraries as I begin understanding the GFX and SSD1306 libraries. 
downloading of them onto my platformio.ini file through using the lib_deps function.

<p align="center"><img src="assests/Journal assests/1.png" width="400"></p>

then an include function was used (#include) to include the aurdino framework, wire, GFX and SSD1306 to incorprete them in src/main where i then defined the dimeansions of the image which were a standered 128 by 64.

<p align="center"><img src="assests\Journal assests\2.png" width="500"></p>

Where I used an LCD converter to convert my image into a C file, which contained monochromatic information about the image, which was then used to display it on the OLED 0.96-inch this was shown in [assests/image.c](assests\Image.c) showcasing an BLINKS mascot where I used.

<p align="center"><img src="assests/Journal assests/3.png" width="500"></p>

the next step was fairly easy as it was th wiring using an esp32-WROOM-32 as the microcontroller and an OLED 0.96" LCD,I2C display. following the defult wiring for L2C.


GND: GND, 3V3: VCC, D21: SDA, D22: SCL

---
### Day 2 - animating the mascot
Day 2 primarily focused on creating an idle animation GIF file following the construction of the mascot as well as the wiring of the ultrasonic sensor. The process of creating a GIF was straightforward, although it was tedious due to the downsizing of the actual mascot image. The mascot had to be redrawn with a lower resolution of 128x64, resulting in way fewer colors existing as well as a lot of details getting lost.

which resulted in an unclear gif on the oled display due to the colors becoming monocramatic this was easily solved by enabling dithering.

<p align = "center"> <img src = "assests/Journal assests/comparison between dithering and not dithring.png"  width="350"></p>

this allows gradients to take place although it looks distorted at first glance it becomes very visable with small screens such as the one used in this project (I2C 0.96" oled display).
<table>
<tr>
<td width="40%">The idle animation featured a breathing animation. The breathing animation featured a blinking animation, quite frankly, due to the whole project being named Blink, as well as the character going up and down. This is a technique used by most pixel art artists to give the illusion of breathing. 
the gif was drawn and animated using piskel a free open-source pixel animation editor.
</td>
<td width="60%"> <p align="center"><img src="assests/Journal assests/Idle animation.gif" width="200"></p>
</td>
</tr>
</table>


<table>
<tr>
    <td width="40%">the wiring of the ultrasonic sensor consists of a voltage divider that turns the ECHO pin voltage outpot of 5v into a safe 3v voltage that the esp32 could handel, this was done through a combination of a 220Ω and 330Ω. 
    
where R1 is the 220Ω connecting 2 breadboard columns together and R2 (the one connect to the GND) is 330Ω and both of them being connected in the same colum creats something called resistor junction, this was done due to the ultrasonic sensor need for a 5v input which is given to it through the VIN pin but due to the esp32 input being 3.3v when the echo pin outputs its voltage it need to reach the esp32 as >= 3.3v which is ultimetly done through the resistor junction.

</td>
    <td width="60%"> <img src="assests/Journal assests/Basic ultrasonic sensor wiring.png" ></td>
</tr>
</table>



---
### day 3 - more gifs!!
Day 3 mainly consisted of desiging multiple gif animations these gif animations included 
<table>
<tr>
    <td width="60%">a confused animation while the mascot is still in "uniform".</td>
    <td width="40%"> <img src="assests/Journal assests/'huh' animation (normal outfit).gif"></td>
</tr>

<tr>
    <td width="30%">a confused animation as to why he was waken up.</td>
    <td width="70%"> <img src="assests/Journal assests/'huh' animation (pijames).gif"></td>
</tr>

<tr>
    <td width="60%">a surprised animation where the mascot is surprised (after a prolonged session of desk use without standing up)</td>
    <td width="40%"> <img src="assests/Journal assests/Surprised animation.gif"></td>
</tr>

<tr>
    <td width="60%">a running animation when user has been working for sometime.</td>    
    <td width="40%"> <img src="assests/Journal assests/Running animation.gif"></td>

</tr>
<tr>
    <td width="60%">a sleeping animation for when blink isn't active (the user is not near his desk for prolonged time)</td>
    <td width="40%"> <img src="assests/Journal assests/sleeping animation.gif"></td>
</tr>

<tr>
    <td width="60%">a flaberrgasted animation when user spends alot of time using his desk generally
    <td width="40%"> <img src="assests/Journal assests/falbergasted ( reached 8 hours of work ).gif"></td> 
</tr>
</table>

these animation are going to be used conditionaly meaning that they are affected by there surronding this is done through the wiring of the ulrasonic sensor and general time.
*note that: every animation so far was drawn in piskel using an xp-pen but the same effects could be reached through using a mouse

---
### Day 4 - State machines
after drawing the GIF it came down to changinig the charcter states based on diffrent interactive conditions this was done by identifying what each gif was for. this was done on two rounds the written pseudocode and the graphed pseudocode.
the logic was done so that the idle state would be the starting state of any session and depending on the interactions it would follow the following logic tree:
<p align="center"><img src="assests/Journal assests/State machine logic.png" width="400"></p>

my first intution was using if conditions and for loops but i founded out that this wouldn't work due to the amount of if conditions and hierachel conditions it would be heavy on the esp32s' cpu and will take alot longer to code so i opted to using a state machine specifically a non-blocking state machine.

state machines are alot easier as it doesn't require me to keep calling on the frame individually as i used to do when testing the idle gif on day 2. 
<img src ="assests/Journal assests/image of the previous code.png">
*sorry for the image begin a commit history it was taken after the code was changed :3

this was done through assigning multiple frames to one array and recalling that array whenever needed whcih is faster and more effecient than calling the gif frame by frame.

### Day 5/6 - more state machine ?!
today consisted mostly of fixing some of the bugs found in the state machine such as the flabergasted state being unreachable or the surprised animation being impossiable to reach.
this was mostly due to incorrect logic as the time used to reach the surprised state was previously the current time or the entry time as the start time restarting the action meaning that it would endlessly run until flabergasted or it went to sleep/ the where did you go animation.
this was fixed in the new ittiration making the flabergasted animatino occuer after 6 hours of running (the continounity of the runnning isn't a must) for 10 min. before defulting to idle.


<p align="center"><img src = "assests/Journal assests/the new state machine logic.png" width="800"></p>

### DAY 7 - i can smell the end !! (pcb and CAD files)
today mostly consisted of me creating the pcb that was dieractly copied from the breadboard demo this was moderlty easy except for checking that everything was running correctly as some concepts were fairly new to me for example net gnd as i had to connect every electronic to the same GND which was done through using the GND symbol paired with a pwr_flag.

<p align="center"><img src="assests/PCB images/pcb electronic symbol.png" width="500"></p>

this was then used to create the footprint which was done through kicad as well, this was easir than the previous step due to the connection already being marked for me in which after a GND ground net was poured using B.CU on the PCB to allow for a net GND throguh the whole pcb.

<p align="center"><img src="assests/PCB images/pcb footprint.png"></p>


with this being the final results (some step files were missing but they are used for cosmetic purposes only)

<p align="center"><img src="assests/PCB images/3d viewer.png"></p>

which this pcb is going to live in this casse designed based on rough mesurments of the hc-sro4 and oled 0.96" ssd1306 I2C screen 

<img src="assests/CAD  images/cover 3-4 view.png" width="482">
<img src="assests/CAD  images/noncover view.png" width="500">

---

<h1 style="text-align: center;"> ENJOY BLINK!! </h1>

*T-T finally
