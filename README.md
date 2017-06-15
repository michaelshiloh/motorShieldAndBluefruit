# motorShieldAndBluefruit

## Combining the Adafruit Motor Shield V2 for Arduino with the 
Adafruit Bluefruit LE SPI Friend

First make sure that no pins conflict. Studying the documentation, we find that:

* Adafruit Motor Shield V2 uses the two I2C pins (SCA and SDL). On an Arduino
Uno these are on pins A4 and A5. If you plan to attach servo motors to the
shield, this uses pins 9 and 10 additionally.

* Adafruit Bluefruit LE SPI Friend uses SPI. According to the [wiring
* diagram](https://learn.adafruit.com/introducing-the-adafruit-bluefruit-spi-breakout/wiring)  
  the default wiring would use pins 4, 7, 8, 11, 12, and 13. (This can be
	changed, see the documentation)

You can mount a header for the Bluefruit module in the prototyping area of 
the motor shield (image TBA)

