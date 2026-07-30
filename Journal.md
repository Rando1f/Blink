---
Title: BLINK
Author: Rando1f
Description: a desk companion montiring desk time with an artistic flair
Created_at: 27 / 7 / 2026
---
#### Total time spent: 6 hours
---
### Day 1 - getting started

Day one was primarily utilized through understanding the fundamentals of C and C++ Mainly void setup and void loop to understand how code is written and how I could write it in the future in order to use it properly, this was paired with acquiring knowledge about libraries as I begin understanding the GFX and SSD1306 libraries. 
downloading of them onto my platformio.ini file through using the lib_deps function.

![NA](<assests/Journal assests/1.png>)

then an include function was used (#include) to include the aurdino framework, wire, GFX and SSD1306 to incorprete them in src/main where i then defined the dimeansions of the image which were a standered 128 by 64.

![the intillized lib](<assests\Journal assests\2.png>)

Where I used an LCD converter to convert my image into a C file, which contained monochromatic information about the image, which was then used to display it on the OLED 0.96-inch this was shown in [assests/image.c](assests\Image.c) showcasing an BLINKS mascot where I used 
![image display code ](<assests/Journal assests/3.png>)

the next step was fairly easy as it was th wiring using an esp32-WROOM-32 as the microcontroller and an OLED 0.96" LCD,I2C display. following the defult wiring for L2C.


GND: GND, 3V3: VCC, D21: SDA, D22: SCL
---
### Day 2 - animating the mascot
Day 2 primarily focused on creating an idle animation GIF file following the construction of the mascot. The process of creating a GIF was straightforward, although it was tedious due to the downsizing of the actual mascot image. The mascot had to be redrawn with a lower resolution of 128x64, resulting in way fewer colors existing as well as a lot of details getting lost.

which resulted in an unclear gif on the oled display due to the colors becoming monocramatic this was easily solved by enabling dithering.

![dithering effect](<assests/Journal assests/comparison between dithering and not dithring.png>)

this allows gradients to take place although it looks distorted at first glance it becomes very visable with small screens such as the one used in this project (I2C 0.96" oled display).

The idle animation featured a breathing animation. The breathing animation featured a blinking animation, quite frankly, due to the whole project being named Blink, as well as the character going up and down. This is a technique used by most pixel art artists to give the illusion of breathing. 

![idle animation ](<assests/Journal assests/Idle animation.gif>)

the gif was drawn and animated using piskel a free open-source pixel animation editor.