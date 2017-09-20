# motorShieldAndBluefruit

## Combining the Adafruit Motor Shield V2 for Arduino with the Adafruit Bluefruit LE SPI Friend

### If you have not already done so, install the library for the Motor Shield:
1. In Arduino, select **Sketch**, **Include Library**, and then **Manage
Libraries**

2. In the search space type **adafruit motor shield v2**

3. Click in the "Adafruit Motor Shield V2 Library" line and an **Install** button
will appear. Click the **Install** button.

4. Close the Library Manager window

### First make sure that no pins conflict. Studying the documentation, we find that:

* Adafruit Motor Shield V2 uses the two I2C pins (SCA and SDL). On an Arduino
Uno these are on pins A4 and A5. If you plan to attach servo motors to the
shield, this uses pins 9 and 10 additionally.

* Adafruit Bluefruit LE SPI Friend uses SPI. According to the [wiring
	diagram](https://learn.adafruit.com/introducing-the-adafruit-bluefruit-spi-breakout/wiring)
  the default wiring would use pins 4, 7, 8, 11, 12, and 13. (This can be
	changed, see the documentation)

### Construction

Start by drawing a schematic. As you read, there are many options, but
it's usually a good idea to start with the default unless you have a 
good reason to do differently.

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
to the Arduino pins, but the holes next to your header will not automatically
connect to the header. You must make this connection yourself by folding the 
wire on the back side of the board and soldering it to the header pin

![Wiring Diagram](images/bluefruit/diagram.jpg)

Solder in the female header

![75](images/bluefruit/75.jpg)

Before you start soldering the wires in place, think about the order.
Will any wires block holes 
that you later need access to? 

Wire colors are very important! Always use red for 5V and black for ground (or
GND). Don't use these colors for any other connections.

Wire choice is important too: Use 22 AWS solid core wire.

I decided to start with GND and 5V

![77](images/bluefruit/77.jpg)

Don't try to wrap the wires around the pins of the header. There isn't room.
Just bend the wire a little bit to hold it in place while you solder it.

![87](images/bluefruit/87.jpg)
![89](images/bluefruit/89.jpg)

After soldering the wire to the header pin,
cut off the excess very close to the pin. Don't be afraid to take
some solder with it:

![90](images/bluefruit/90.jpg)

Now the 5V wire:

![94](images/bluefruit/94.jpg)

After every step compare what you have done with the original table (not your
schematic or diagram in case you made a mistake there). Plug in the module
and check that the labels on the module corresponds to the pins you are 
connecting.

If others are near you, ask them to double check your work, and offer to 
check theirs in return.

Then I added the three that are in a row: pins 13, 12, and 11:

(picture)

Then CS

(picture)

At this point I realized that the wire from IRQ to pin 7 might
cover the hole next to RST, so I did the wire to RST before the wire 
to IRQ.

(picture)

and finally the wire to IRQ:

(picture)

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


![](images/bluefruit/2.jpg)
![](images/bluefruit/3.jpg)
![4](images/bluefruit/4.jpg)
![5](images/bluefruit/5.jpg)
![6](images/bluefruit/6.jpg)
![7](images/bluefruit/7.jpg)
![8](images/bluefruit/8.jpg)
![9](images/bluefruit/9.jpg)
![10](images/bluefruit/10.jpg)
![11](images/bluefruit/11.jpg)
![12](images/bluefruit/12.jpg)
![13](images/bluefruit/13.jpg)
![14](images/bluefruit/14.jpg)
![15](images/bluefruit/15.jpg)
![16](images/bluefruit/16.jpg)
![17](images/bluefruit/17.jpg)
![18](images/bluefruit/18.jpg)
![19](images/bluefruit/19.jpg)
![20](images/bluefruit/20.jpg)
![21](images/bluefruit/21.jpg)
![22](images/bluefruit/22.jpg)
![23](images/bluefruit/23.jpg)
![24](images/bluefruit/24.jpg)
![25](images/bluefruit/25.jpg)
![26](images/bluefruit/26.jpg)
![27](images/bluefruit/27.jpg)
![28](images/bluefruit/28.jpg)
![29](images/bluefruit/29.jpg)
![30](images/bluefruit/30.jpg)
![31](images/bluefruit/31.jpg)
![32](images/bluefruit/32.jpg)
![33](images/bluefruit/33.jpg)
![34](images/bluefruit/34.jpg)
![35](images/bluefruit/35.jpg)
![36](images/bluefruit/36.jpg)
![37](images/bluefruit/37.jpg)
![38](images/bluefruit/38.jpg)
![39](images/bluefruit/39.jpg)
![40](images/bluefruit/40.jpg)
![41](images/bluefruit/41.jpg)
![42](images/bluefruit/42.jpg)
![43](images/bluefruit/43.jpg)
![44](images/bluefruit/44.jpg)
![45](images/bluefruit/45.jpg)
![46](images/bluefruit/46.jpg)
![47](images/bluefruit/47.jpg)
![48](images/bluefruit/48.jpg)
![49](images/bluefruit/49.jpg)
![50](images/bluefruit/50.jpg)
![60](images/bluefruit/60.jpg)
![61](images/bluefruit/61.jpg)
![62](images/bluefruit/62.jpg)
![63](images/bluefruit/63.jpg)
![64](images/bluefruit/64.jpg)
![65](images/bluefruit/65.jpg)
![66](images/bluefruit/66.jpg)
![67](images/bluefruit/67.jpg)
![68](images/bluefruit/68.jpg)
![69](images/bluefruit/69.jpg)
![70](images/bluefruit/70.jpg)
![71](images/bluefruit/71.jpg)
![76](images/bluefruit/76.jpg)
![78](images/bluefruit/78.jpg)
![79](images/bluefruit/79.jpg)
![80](images/bluefruit/80.jpg)
![81](images/bluefruit/81.jpg)
![82](images/bluefruit/82.jpg)
![83](images/bluefruit/83.jpg)
![84](images/bluefruit/84.jpg)
![85](images/bluefruit/85.jpg)
![86](images/bluefruit/86.jpg)
![88](images/bluefruit/88.jpg)
![91](images/bluefruit/91.jpg)
![92](images/bluefruit/92.jpg)
![97](images/bluefruit/97.jpg)
![98](images/bluefruit/98.jpg)
![99](images/bluefruit/99.jpg)
![100](images/bluefruit/100.jpg)
![101](images/bluefruit/101.jpg)
![102](images/bluefruit/102.jpg)
![103](images/bluefruit/103.jpg)
![104](images/bluefruit/104.jpg)
![105](images/bluefruit/105.jpg)
![106](images/bluefruit/106.jpg)
![107](images/bluefruit/107.jpg)
![108](images/bluefruit/108.jpg)
![109](images/bluefruit/109.jpg)
![110](images/bluefruit/110.jpg)
![111](images/bluefruit/111.jpg)
![112](images/bluefruit/112.jpg)
![113](images/bluefruit/113.jpg)
![114](images/bluefruit/114.jpg)
![115](images/bluefruit/115.jpg)
![116](images/bluefruit/116.jpg)
![117](images/bluefruit/117.jpg)
![118](images/bluefruit/118.jpg)
![119](images/bluefruit/119.jpg)
![120](images/bluefruit/120.jpg)
![121](images/bluefruit/121.jpg)
![122](images/bluefruit/122.jpg)
![123](images/bluefruit/123.jpg)
![124](images/bluefruit/124.jpg)
![125](images/bluefruit/125.jpg)
![126](images/bluefruit/126.jpg)
![127](images/bluefruit/127.jpg)
![128](images/bluefruit/128.jpg)
![129](images/bluefruit/129.jpg)
![130](images/bluefruit/130.jpg)
![131](images/bluefruit/131.jpg)
![132](images/bluefruit/132.jpg)
![133](images/bluefruit/133.jpg)
![134](images/bluefruit/134.jpg)
![135](images/bluefruit/135.jpg)
![136](images/bluefruit/136.jpg)
![137](images/bluefruit/137.jpg)
![138](images/bluefruit/138.jpg)
![139](images/bluefruit/139.jpg)
![141](images/bluefruit/141.jpg)
![142](images/bluefruit/142.jpg)
![143](images/bluefruit/143.jpg)
![144](images/bluefruit/144.jpg)
![145](images/bluefruit/145.jpg)
![146](images/bluefruit/146.jpg)
![147](images/bluefruit/147.jpg)
![148](images/bluefruit/148.jpg)
![149](images/bluefruit/149.jpg)
![150](images/bluefruit/150.jpg)
![151](images/bluefruit/151.jpg)
![152](images/bluefruit/152.jpg)
![153](images/bluefruit/153.jpg)
![155](images/bluefruit/155.jpg)
![156](images/bluefruit/156.jpg)
![157](images/bluefruit/157.jpg)
