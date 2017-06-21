# motorShieldAndBluefruit

## Combining the Adafruit Motor Shield V2 for Arduino with the 
Adafruit Bluefruit LE SPI Friend

### First make sure that no pins conflict. Studying the documentation, we find that:

* Adafruit Motor Shield V2 uses the two I2C pins (SCA and SDL). On an Arduino
Uno these are on pins A4 and A5. If you plan to attach servo motors to the
shield, this uses pins 9 and 10 additionally.

* Adafruit Bluefruit LE SPI Friend uses SPI. According to the [wiring
* diagram](https://learn.adafruit.com/introducing-the-adafruit-bluefruit-spi-breakout/wiring)  
  the default wiring would use pins 4, 7, 8, 11, 12, and 13. (This can be
	changed, see the documentation)

### Construction

You can mount a header for the Bluefruit module in the prototyping area of 
the motor shield (image TBA)

### Software

For a code example, see [this example](motorShieldAndBluefruit/motorShieldAndBluefruit.ino)

### Changing the name of your Bluefruit Friend

If there are many similar devices, you might find it useful to change the 
name of your Bluetooth module:

1. In the Arduino Coding Environment, go to
```File->Examples->Adafruit Bluetooth nRF51->atcommand```

2. Upload to Arduino, then go to serial monitor

3. Type ```AT+GAPDEVNAME=x```, where ```x``` is the new name. 
Note that this is case sensitive (capitolization matters),
and that there must be no spaces.
Type this in the top section of the serial monitor, 
then press send. You should see an ```OK```.

4. Type in ATZ and click send. You should see another ```OK```.

5. The name should now be changed, the Arduino example will issue a factory
reset which will erase the name. To prevent the factory reset,

Find the phrase ```FACTORYRESET_ENABLE``` which will look like this:

#define FACTORYRESET_ENABLE 1  
#define MINIMUM_FIRMWARE_VERSION "0.6.6"  
#define MODE_LED_BEHAVIOUR "MODE"  

Change the 1 to a 0, and this disables factory reset. 

### Providing separate power for servo motors

Adafruit has made it easy to provide separate power to the servo
motors:

1. Carefully cut the 5V trace where indicated on the back of the motor shield.
To make sure there are no slivers of copper remaining, I like to remove a 
small length of copper that I can actually see:

![](images/cutTraceToUseOptionalServoInput.jpg)

2. Install screw terminals in the holes, or solder wires from a 6V battery
pack directly, to the indicated holes. 
Make sure the polarity is correct: **red** is
**positive** and **black** is **negative**:

![](images/motorShieldOptServo_bb.png)

*Note 1*: This provides power to the two servo headers that are pre-installed
on the shield (labelled Servo 1 and Servo 2.)
If you add more headers for more servo motors, 
you will need to add your own connection to this new power connector. 
The ground pin can be the same as the Arduino ground, 
since all grounds are common, 
and the the middle pin (the 5V pin)
should be connected to the middle pin of either of the two 
pre-installed servo headers
(which are now connected to this new power connector).

*Note 2*: The power to the servo motors is separate from the power to the DC
motors. This means more battery packs, and it allows you to have a different
voltage for the DC motors than the servo motors.
