# Software / Programming
The Instructions provide are provide as reference information. Author assumes that you are experience with Arudino software.
Author assumes **NO** responsibility for any programming mishaps.

Original GPS clock [document](http://w8bh.net/gps_clock.pdf) from W8BH. 

### 1. Setting up the Arduino IDE
Portions of this section maybe omitted if you already have Arduino IDE installed.  

* Download the latest Arduino IDE software for you platform from [here](https://www.arduino.cc/en/Main/Software) and install it.
* Add the STM32 Boards to Arduino Board [library](https://github.com/stm32duino/Arduino_Core_STM32/wiki/Getting-Started)
* Install the following [modules](https://github.com/kj7dz/GPS-clock/blob/main/images/IDE%20modules.jpg) to the Aruduino IDE "Library Manager"
	* **TFT_eSPI** by [Bodmer](https://github.com/Bodmer/TFT_eSPI)
	* **Time** [Michael Margolis](https://github.com/PaulStoffregen/Time)
	* **Timezone** by [Jack Christensen](https://github.com/JChristensen/Timezone)
	* **TinyGPSPlus** by [Mikal Hart](https://github.com/mikalhart/TinyGPSPlus)
 * You will also need to install [STM32CubeProgrammer software](https://www.st.com/en/development-tools/stm32cubeprog.html#get-software)
   
### 2. Setting up the GPS sketch 
In this section you need to configure the sketch parameters prior to uploading to the ST32M development board module.  

* Download the GPS sketch file from [here](https://github.com/kj7dz/GPS-clock/blob/main/Sketch%20code/GPS_Clock_Triplel_STM_32.ino) and save it locally.
* Launch Arduino IDE software and open the GPS sketch file you downloaded.
* Looking at this [image](https://github.com/kj7dz/GPS-clock/blob/main/images/GPS%20sketch.jpg), verfiy you have the correct timezone settings the sketch.  The sketch is **Pacific Time Zone**.
```css
TimeChangeRule EDT                                 // Timezone setup for EST/EDT.
  = {"EDT", Second, Sun, Mar, 2, -240};            // Set Daylight time here.  UTC-4hrs
TimeChangeRule EST                                 // For ex: "First Sunday in Nov at 02:00"
  = {"EST", First, Sun, Nov, 2, -300};             // Set Standard time here.  UTC-5hrs
TimeChangeRule *tz;                                // pointer to current time change rule
Timezone myTZ(EDT, EST);                           // create timezone object with rules above
```
```css
TimeChangeRule CDT                                 // Timezone setup for CST/CDT.
  = {"CDT", Second, Sun, Mar, 2, -300};            // Set Daylight time here.  UTC-5hrs
TimeChangeRule CST                                 // For ex: "First Sunday in Nov at 02:00"
  = {"CST", First, Sun, Nov, 2, -360};             // Set Standard time here.  UTC-6hrs
TimeChangeRule *tz;                                // pointer to current time change rule
Timezone myTZ(CDT, CST);                           // create timezone object with rules above
```
```css
TimeChangeRule MDT                                 // Timezone setup for MST/MDT.
  = {"MDT", Second, Sun, Mar, 2, -360};            // Set Daylight time here.  UTC-6hrs
TimeChangeRule MST                                 // For ex: "First Sunday in Nov at 02:00"
  = {"MST", First, Sun, Nov, 2, -420};             // Set Standard time here.  UTC-7hrs
TimeChangeRule *tz;                                // pointer to current time change rule
Timezone myTZ(MDT, MST);                           // create timezone object with rules above
```
```css
TimeChangeRule PDT                                 // Timezone setup for PST/PDT.
  = {"PDT", Second, Sun, Mar, 2, -420};            // Set Daylight time here.  UTC-7hrs
TimeChangeRule PST                                 // For ex: "First Sunday in Nov at 02:00"
  = {"PST", First, Sun, Nov, 2, -480};             // Set Standard time here.  UTC-8hrs
TimeChangeRule *tz;                                // pointer to current time change rule
Timezone myTZ(PDT, PST);                           // create timezone object with rules above
```
* Also replace **URCALL** with your CALL Sign. (do not remove the quotes)
* Compile your sketch and verify that there are NO errors.
* **Save your GPS sketch!!**

## 3. Setting board parameters in Arduino IDE
For the boards settings, follow the instructions below and verify [here](https://github.com/kj7dz/GPS-clock/blob/main/images/Board%20Settings.png)
* From the Tools -> Board -> STM32 boards (set to) -> Generic STM32F1
* From the Tools -> Board -> Board Part Number -> Blue Pill F103CB (or C8 with 128k)
* From the Tools -> Upload Method -> STM32CubeProgrammer (SWD)
## 4. Programming the STM32 module
Using the ST-Link V2 USB programmer module, connect it to the STM32 as follows.
* With the 4-wire cable, [attached them](https://github.com/kj7dz/GPS-clock/blob/main/images/Programmer%201.png) to the corresponding pins:

|ST-Link | Cable| STM32 (4 pin header) |
| --- | - | --- |
| 3.3V |  - | 3.3V |
| GND  | - | GND |
| SWDIO | - | DIO |
| SWCLK | - | CLK | 
* Connect the ST-LINK to an open USB port
	* In Windows device Manager, you should see the [following](https://github.com/kj7dz/GPS-clock/blob/main/images/Device%20Mgr.jpg) STM32 STLink device.
* Launch the Arduino IDE program
* Load the GPS sketch with the changes
* Click on the green circle with check mark in it to verify the sketch.  Fix if there are errors.
	* If you get **TOUCH_CS pin not defined** error, in the **/libaries/TFT_eSPI/User_Setup.h** file, uncomment **# define TOUCH_CS PIN_D2**
* Click on the green circuit with arrow in it and watch the log file for a successfull upload.
* Disconnect the STM32 from the ST-Link
* Install the STM32 back on the PCB, make sure the USB port faces towards the power connector.
* Enjoy!!
  

