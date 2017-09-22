# motorShieldAndBluefruit

# Combining the Adafruit Motor Shield V2 for Arduino with the Adafruit Bluefruit LE SPI Friend

Start by reading the Adafruit
documentation for the [motor
shield](https://learn.adafruit.com/adafruit-motor-shield-v2-for-arduino/using-dc-motors?view=all) and the [Bluefruit module](https://learn.adafruit.com/introducing-the-adafruit-bluefruit-spi-breakout?view=all)

There are many confusing options but try to get the broad concept.

## Construction

### Planning

First make sure that no pins conflict. Studying the documentation, we find that:

* Adafruit Motor Shield V2 uses the two I2C pins (SCA and SDL). On an Arduino
Uno these are on pins A4 and A5. If you plan to attach servo motors to the
shield, this uses pins 9 and 10 additionally.

* Adafruit Bluefruit LE SPI Friend uses SPI. According to the [wiring
	diagram](https://learn.adafruit.com/introducing-the-adafruit-bluefruit-spi-breakout/wiring)
  the default wiring would use pins 4, 7, 8, 11, 12, and 13. (This can be
	changed, see the documentation)

Since there are no pins used by both devices, we can use the default wiring.

The motor shield can not be changed, but the Bluefruit module
can be wired differently. 
Unless you have a good reason to do differently,
it's usually a good idea to start with the default.

Start by drawing a schematic. 

I started with
[this](https://learn.adafruit.com/introducing-the-adafruit-bluefruit-spi-breakout/wiring#default-pinout)
table in the Adafruit guide. Note that they don't list the DFU pin (since it
isn't used) but I added it to my schematic to remind me not to use it:

![](images/bluefruit/73.jpg)

You can mount a header for the Bluefruit module in the prototyping area of 
the motor shield 

Think about where you want the module to sit. Since some of the wires
connect directly to pins 13, 12, and 11, it might be convenient to put it 
nearby. Leave room for making your connections. I left only one row, you might
want to leave more so that it's not so tight. Put the header 
and Bluetooth module in loosely while you experiment to
help you visualize:

![72](images/bluefruit/72.jpg)

Before you start soldering, draw a diagram of how you will make the 
connections. Think about where the wires will go. 

Remember that the holes next to the Arduino pins are automatically connected
to the Arduino pins, but the holes next to your header will *not* automatically
connect to the header. You must make this connection yourself by folding the 
wire on the back side of the board and soldering it to the header pin

![Wiring Diagram](images/bluefruit/diagram.jpg)

### Soldering

Before you start soldering the wires in place, think about the order.
Will any wires block holes 
that you later need access to? 

**Wire colors are very important! Always use red for 5V and black for ground (or
GND). Don't use these colors for any other connections.**

**Wire choice is important too: Use 22 AWS solid core wire.**

1. Solder in the female header

	![75](images/bluefruit/75.jpg)

1. I decided to start with GND and 5V. First GND:

	![77](images/bluefruit/77.jpg)

1. Don't try to wrap the wires around the pins of the header. There isn't room.
	Just bend the wire a little bit to hold it in place while you solder it.

	![87](images/bluefruit/87.jpg)
	![89](images/bluefruit/89.jpg)

	After soldering the wire to the header pin,
	cut off the excess very close to the pin. Don't be afraid to take
	some solder with it:

	![90](images/bluefruit/90.jpg)

	If you make a mistake, it is usually easier to cut the wire in half and
	to remove each piece separately. 


	![141](images/bluefruit/141.jpg)
	![142](images/bluefruit/142.jpg)

	Think about how the wire is bent and 
	wiggle it gently to unbend it while heating the solder with
	the soldering iron. You can use the soldering iron tip gently
	to help unbend the wires. Try not to use too much force as this might 
	damage the board.

1.	Now the 5V wire:

	![94](images/bluefruit/94.jpg)

	After every step compare what you have done with the original table (not your
	schematic or diagram in case you made a mistake there). Plug in the module
	and check that the labels on the module corresponds to the pins you are 
	connecting.

	If others are near you, ask them to double check your work, and offer to 
	check theirs in return.

1.	Then I added the three that are in a row: pins 13, 12, and 11:

	![120](images/bluefruit/120.jpg)
	![121](images/bluefruit/121.jpg)

	Check each solder joint as you make it that it is nice and shiny and that 
	you haven't accidentally soldered two pins together.

	As you solder each wire, remember to trim off the excess wire very close:

	![124](images/bluefruit/124.jpg)

1. Then CS. Remember that it goes to Arduino pin 8 so make it a little longer
	and double check that you have it in the right holes before you solder:

	![132](images/bluefruit/132.jpg)

1.	At this point I realized that the wire from IRQ to pin 7 might
	cover the hole next to RST, so I did the wire to RST before the wire 
	to IRQ. Remember that you have to skip the DFU pin so think carefully
	and make sure your diagram, your wire, the label on the Arduino pin, the label
	on the Bluefruit module, and the default wiring table are all in
	agreement
	before you solder.

	![138](images/bluefruit/138.jpg)

1. and finally the wire to IRQ:

	![148](images/bluefruit/148.jpg)

1.	Inspect all your solder joints carefully. Make sure all the joints are shiny
	and complete, that the solder flows smoothly over the wire and over the pins.
	Make sure there isn't too much solder, and make sure solder doesn't "bridge"
	two (or more) adjacent pins together.

	![150](images/bluefruit/150.jpg)

1.	For many more pictures of the assembly process look [here](extraImages.md)

1. When you plug in your module, make sure it's the right way around. 
Connect power to the wrong pins can damage your module. I usually look 
for the red and black wires (which I know are 5V and GND) to go to the
side of the module with the VIN and GND pins.

Think carefully before you turn anything on: did you make any mistakes?


## Software

Before writing any of your own code, test that each device works 
independently with the built in examples

### Motor Shield

#### Install the Motor Shield library

1. In Arduino, select **Sketch**, **Include Library**, and then **Manage
Libraries**

2. In the search space type **adafruit motor shield v2**

3. Click in the "Adafruit Motor Shield V2 Library" line and 
an **Install** button will appear. Click the **Install** button.

4. Close the Library Manager window

6. Open the simple example
**File** -> **Examples** -> 
**Adafruit Motor Shield V2 Library** ->
**DCMotorTest**

5. Test that the library was correctly installed by verifying (compiling)
the example by pressing the **Verify** button, which is just to the left 
of the **Upload** button

#### Testing the Motor Shield

5. You will be following
[these](https://learn.adafruit.com/adafruit-motor-shield-v2-for-arduino/using-dc-motors?view=all#dc-motor)
steps.

6. Connect a motor to the two pins labeled M1 on the motor shield 
as shown in [this](https://learn.adafruit.com/assets/9471) picture

7. For this test you can power the motor from your Arduino, but 
for reliable project operation it is better to use a separate power supply.
To use the Arduino power, simply insert the provided shorting block on the
two pins labeled **VIN Jumper** as shown in
[this](https://learn.adafruit.com/assets/9472) picture.

8. Upload the 
**DCMotorTest**
example. The motor should turn back and forth as explained
at the end of 
[this](https://learn.adafruit.com/adafruit-motor-shield-v2-for-arduino/using-dc-motors?view=all#dc-motor).
section.

9. Remove the shorting block from the
[**VIN Jumper**](https://learn.adafruit.com/assets/9472) 
because from now on you should use separate power for any motors


### Bluefruit SPI Friend

#### Install the Bluefruit SPI Friend library

1. In Arduino, select **Sketch**, **Include Library**, and then **Manage
Libraries**

2. In the search space type **adafruit nrf51**

3. Click in the 
"Adafruit BluefruitLE nRF51"
line and an **Install** button will appear. Click the **Install** button.

4. Close the Library Manager window

6. Open the simple example
**File** -> **Examples** -> 
**Adafruit BluefruitLE nRF51**
**controller**

5. Test that the library was correctly installed by verifying (compiling)
the example by pressing the **Verify** button, which is just to the left 
of the **Upload** button.

### Testing the Bluefruit SPI Friend

5. You will be following
[these](https://learn.adafruit.com/introducing-the-adafruit-bluefruit-spi-breakout?view=all#controller)
steps.

8. Upload the 
**Controller**
example. Note that the serial port is opened at a different speed (baud rate)
than we usually use.

9. Open your serial monitor and change the baud rate to agree with the 
one in the example. If you forget this step your serial monitor might not show
anything, or it might show random characters.

10. Download and install the 
**Adafruit Bluefruit LE Connect app** for
[iOS](https://learn.adafruit.com/bluefruit-le-connect-for-ios)
or for
[Android](https://play.google.com/store/apps/details?id=com.adafruit.bluefruit.le.connect&hl=en)
to your phone

11. Open the app on your phone and 
connect to your Adafruit Bluefruit LE device. You should see some activity
on your serial monitor and the blue light on your Bluetooth module may
illuminate.

12. You might be asked to update the firmware. This is safe and recommended.
This process might take a good 5-10 minutes (depending on network speed)
so be patient. If you update firmware your phone might disconnect and ask you to
reconnect. If so, repeat the step above.

12. Once you are connected select **Controller** and then scroll down and
select the **Control Pad Module**. Now we are following
[these](https://learn.adafruit.com/introducing-the-adafruit-bluefruit-spi-breakout?view=all#control-pad-module)
steps. 

13. Press the buttons and observe the correct messages appear in your serial
monitor.


### Combining the Motor Shield and the Bluefruit SPI Friend

It is best, I think, to start with the Bluefruit Controller built-in 
example. Scroll down in the code to where the buttons are detected:

```    // Buttons
    if (packetbuffer[1] == 'B') {
      uint8_t buttnum = packetbuffer[2] - '0';
      boolean pressed = packetbuffer[3] - '0';
      Serial.print ("Button "); Serial.print(buttnum);
      if (pressed) {
        Serial.println(" pressed");
      } else {
        Serial.println(" released");
      }
    }
```

Basically, you will be adding code that responds to specific buttons
using the `buttnum` variable and deciding what you want your 
motors to do based on whether that button was pressed or released (the
`pressed` variable).

For a code example, see [this example](code/motorShieldAndBluefruit/motorShieldAndBluefruit.ino)

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

# Providing separate power for servo motors

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


