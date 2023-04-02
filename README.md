# This is an Arduino RC engine sound generator with light simulation

I am new at learning arduino and currently only have arduino nano spare around so i try to continue TheDIYGuy999 deprecated works.<br>
My main aim is to have sound and light controller for my rc<br>
Any help to fine tune the code really apreciated.<br>

## Source
Deprecated project v1.33 of TheDIYGuy999<br>
GitHub repo: https://github.com/TheDIYGuy999/Rc_Engine_Sound <br>
It's based on the mojoEngineSim: https://github.com/BeigeMatchbox/mojoEngineSim <br>
<br>
his new ESP32 version: https://github.com/TheDIYGuy999/Rc_Engine_Sound_ESP32 <br>

## Features:
- Many selectable engine sounds and startup sounds for cars and trucks
- Sound files up to 8bit, 16kHz, mono can be used
- Works best with a PAM8403 amplifier module, connected to pin 3, via a 10kOhm potentiometer
- The engine RPM is calculated according to RC signal input on pin 2
- Gear shifting is simulated in "curves.h"
- Use an Arduino Pro Pro 5V, 16MHz
- Light simulation

## Part List
- Arduino nano / mini / uno
- PAM8403 mini amplifier
- potentiometer 10k
- resistor
- speaker (max 3 watt)
- 2 x 5 mm led white (head lamp)
- 2 x 3 mm led white (reverse lamp)
- 2 x 3 mm led red (stop/brake lamp)
- 4 x 3 mm led yellow (sign/blink lamp)

## how to use
- Open the "Rc_Engine_Sound.ino" and choose the "settings.h" tab
- select the sound that you want by commenting/uncomment the sound file
- additionaly you can change the Gear shifting in the "curves.h"
- connect the speaker and hardware to:
  -  Speaker to 3
  -  receiver/remote Ch1 to 4
  -  receiver/remote Ch2 to 2
  -  receiver/remote Ch3 to 6
  -  brake lamp to A1
  -  reverse lamp to A2
  -  head lamp to A3
  -  Signal left A4
  -  Signal right A5
- upload the file to your board
- if the light is jittery then change the pulse value in the "Rc_Engine_Sound.ino" 

### search for pulse value
- open the "Rc_Engine_Sound.ino"
- go to "void loop()" choose the ch you want to find the value and uncomment the "Serial.print" and "Serial.println"
- upload and open the serial monitor
- best if you uncomment 1 channel at a time and play with automtic scrolling
- changes the value at //Head Lamp and //signal lamp     

## Schematic:
![](https://github.com/projectronic/Arduino_Rc_Engine_Sound_with_light/blob/52771ad485f95c72b8efa5ffc7c4e6dda670866b/doc/Schematic_bb.png)
![](https://github.com/projectronic/Arduino_Rc_Engine_Sound_with_light/blob/52771ad485f95c72b8efa5ffc7c4e6dda670866b/doc/led%20wiring_bb.png)

## Ho to create new sound arrays:

### Audacity:
- Import the sound file you want in Audacity
- Convert it to mono, if needed
- on the bottom left, select project frequency 16000kHz
- cut the sound to one engine cycle. Zoom in to find the exact zero crossing
- adjust the volume, so that the entire range is used
- select > export audio > WAV > 8-bit-PCM
- note, that the files should be as short as possible: around 0.3s for idle and 1s for start

### Loading and compiling wav2c (this is for OS X):
- download it from: https://github.com/olleolleolle/wav2c
- compile it in terminal with the following steps:
- type "gcc" and space
- drag and drop the files "main.c", wavdata.h", wavdata.c" into the terminal window.
- press enter -> the executable is then compiled and stored as "youruserdirectory/a.out"

### Processing the new header file with your sound:
- copy an existing "enginesound.h" file, rename it with your new engine name
- drag and drop "a.out" into your terminal
- drag and drop the exported WAV file into your terminal
- drag and drop your copied "enginesound.h" file into your terminal
- type "idle" for the idle file or "start" for the start file
- press enter -> the "enginesound.h" file is now overwritten with the new sound data.
- uncomment the line "sampleRate"
- change "signed char" to "unsigned char"
- include this file in "settings.h"

### Compiling the new sketch:
- compile and upload the sketch in Arduino IDE
- the new engine should now run...

## Breadboard

![](https://github.com/projectronic/Arduino_Rc_Engine_Sound_with_light/blob/1e557189ca2686f27630be6b2f0db9ebb6b8d92d/doc/photo_2023-04-03_00-57-10.jpg)
![](https://github.com/projectronic/Arduino_Rc_Engine_Sound_with_light/blob/1e557189ca2686f27630be6b2f0db9ebb6b8d92d/doc/photo_2023-04-03_00-57-04.jpg)
![](https://github.com/projectronic/Arduino_Rc_Engine_Sound_with_light/blob/1e557189ca2686f27630be6b2f0db9ebb6b8d92d/doc/photo_2023-04-03_00-56-59.jpg)
![](https://github.com/projectronic/Arduino_Rc_Engine_Sound_with_light/blob/1e557189ca2686f27630be6b2f0db9ebb6b8d92d/doc/photo_2023-04-03_00-56-43.jpg)
