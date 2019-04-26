![](https://img.shields.io/badge/CBPi%203%20addin-functionable-green.svg)  ![](https://img.shields.io/github/license/JamFfm/craftbeerpiLCD.svg?style=flat) ![](https://img.shields.io/github/last-commit/JamFfm/craftbeerpiLCD.svg?style=flat) ![](https://img.shields.io/github/release-pre/JamFfm/craftbeerpiLCD.svg?style=flat)

# **LCD add-on for CraftBeerPi 3**

![](https://github.com/breiti78/craftbeerpiLCD/blob/master/LCDPhoto.jpg "LCDDisplay Default Display")

With this add-on you can display your Brewing steps temperatures on a 20x4 i2c LCD Display.
In addition you can display the target-temperatur and current-temperature of each fermenter.
This addon only works with I2C connected LCD Displays.

## Installation

Download and install this plugin via 
the CraftBeerPi user interface. It is called LCDDisplay.
After that a reboot is necessary.

## Configuration

At least configure your i2c adress in the parameters menue. Some other
parameters of the LCD can be changed in the  __init__.py file in the
/home/pi/craftbeerpi3/modules/plugins/LCDDisplay folder.


There are different modes:

**Defaultdisplay**
--------------

If no brewing process is running the LCD Display will show

- CraftBeerPi-Version 
- Brewery-name
- Current IP adress 
- Current date/time

**Multidisplay mode**
-----------------

- The script will loop thru your kettles and display the target and current temperatur. 
- If heater is on, a beerglas symbol will appear in the first row on the right side (not flashing).
- When target-temperature is reached it displayes the remaining time of the step (rest) too.

**Single mode**
-----------

- Only displayes one kettle but reacts a little bit faster on temperature changes. 
- It displayes the remaining time of the step (rest) when target temperature is reached.
- When the heater is "on" a small beerglas is flashing on/off in the first row on the right side.

**Fermenter mode**
--------------
- Pretty much the same as multidisplay for all fermenter.
- Displayes the brewname, fermentername, target-temperature, current-temperature of each fermenter.
- When the heater or cooler of the fermenter is on it will show a symbol.
A beerglas detects heater is on, * means cooler in on.
- The remaining time for each fermenter is shown like in weeks, days, hours. 
- Fermenter mode starts when a fermenter-step of any of the fermenters is starting and no brewing step is running(most likely)

Parameter
---------

There are several parameter to change in the **CBPi-parameter** menue:


**LCD_Adress:**    
This is the adress of the LCD modul. You can detect it by 
using the following command in the commandbox of the Raspi:   
- sudo i2cdetect -y 1 
or 
- sudo i2cdetect -y 0.
Default is 0x27.
 
 
**LCD_Multidisplay:**     
Changes between the 2 modes. "on" means the Multidisplaymode is on. 
"off" means singledisplaymode is on. Default is "on". 


**LCD_Refresh:**		  
In Multidisplay mode this is the time to wait until switching to next displayed kettle. 
Default is 5 sec.
 

**LCD_Singledisplay:** 	  
Here you can change the kettle to be displayed in single mode. The number is the same as row number  of
kettles starting with 1. Default is kettle 1 (probably the first kettle which was defined in hardware).



## Hints

- Changing a LCD_xxxx parameter in the parameters menue or any
file in LCDDisplay folder usually requires a reboot.
- Whether you need a reboot have a look in the comments of the parameters.
- A new fermenter should have a target temperature and at least one step defined.
- It maybe necessary to restart craftbeerpi after adding a new fermenter. 
- Sometimes it lastes a long time till the fermenterstep starts running. 
I don't know why this is happening.
- If the address is right but you still can not see letters displayed:
  - try to adjust contrast by the screw on the back of the LCD Hardware (I2C Modul)
  - be shure to provide the LCD hardware with the right ammount of voltage (mostly 5V or 3.3V)
  - use a strong powersuppy. If you notice LCD fading a bit there is a lack of current.
  - use proper connections. Soldering the wires is best for connection. Bad connection can also result in fading the LCD.


## Known Problems
The LCD does not like temperature below 0°C (32°F). It becomes slow and can be damaged like brightness is no more homogen throughout the hole LCD area.

When CBPi3 Mesh Steps are active and you restart CBPi3 the display will show nothing. Stop and restart the Mesh steps.


## Questions  
Questions can be posed in the Craftbeerpi Usergroup in Facebook or in the repository.


## Fixed Issues
Now the °C or F is displaed like in CBPi parameters
If there is a missing Kettle or Fermenter no more faults are thrown.

