# Software 
The Instructions provide are provide as reference. Author assumes **NO** responsibility for any programming mishaps.

### 1. Setting up the Arduino IDE
Portions of this section maybe omitted if you already have Arduino IDE installed.  

* Download the latest Arduino IDE software for you platform from [here](https://www.arduino.cc/en/Main/Software) and install it.
* From File -> Preferences, add the following string to "Additional boards manager URLs" box.
```css
https://github.com/stm32duino/BoardManagerFiles/raw/main/package_stmicroelectronics_index.json
```
* Add the following [modules](https://github.com/kj7dz/GPS-clock/blob/main/images/IDE%20modules.jpg) to the Aruduino IDE "Library Manager"
	* **TFT_eSPI** by Bodmer
	* **Time** Michael Margolis
	* **Timezone** by Jack Christensen
	* **TinyGPSPlus** by Mikal Hart 		
### 2. Setting up the GPS sketch 
In this section you need to configure the sketch parameters prior to uploading to the ST32M development board module.  

* Download the GPS sketch file from [here](https://github.com/kj7dz/GPS-clock/blob/main/Sketch%20code/GPS_Clock_Triplel_STM_32.ino) and save it locally.
* Launch Arduino IDE software and open the GPS sketch file.
* Change line 57 - 62 to match your timezone.  Sketch is already set to **Pacific Time Zone**.
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
	 
* Scroll down to line 64
	* Replace URCALL with your CALL Sign. (do not remove the quotes)
* Compile your sketch and verify that there are NO errors.

## 3. Setting board parameters in Arduino IDE

* From the Tools -> Board -> STM32 boards (set to) -> Generic STM32F1
* From the Tools -> Board -> Board Part Number -> Blue Pill F103CB (or C8 with 128k)
* From the Tools -> Upload Method -> STM32CubeProgrammer (SWD)
*  

