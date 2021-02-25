## grblHAL plugins

grblHAL's HAL interface is based on function pointers that may be used to add functionality without any need to change the core grbl code. They may also be changed on the fly to redirect calls, eg. the SD-card interface utilizes this to temporarily redirect input from the serial stream to the SD card.

NOTE: A plugin needs to be supported by the processor specific driver - as a minimum a initialization call has to be made. 

* [EEPROM](../Plugin_EEPROM/README.md) - for non-volatile storage of settings/data on an external EEPROM or FRAM.

* [Encoder](../Plugin_encoder/README.md) - for adjusting overrides<sup>1</sup>. Support for jogging is planned.

* [Keypad](../Plugin_I2C_keypad/README.md) - for I2C based keypad<sup>1</sup>. Support for jogging etc. [This](https://github.com/terjeio/I2C-interface-for-4x4-keyboard) is an example of an implementation.

* [Networking](../Plugin_networking/README.md) - for telnet or websocket communication<sup>2</sup>.

* [Odometer](../Plugin_odometer/README.md) - for logging of distances travelled and machining time. __NOTE:__ For review.

* [Plasma/THC](../Plugin_plasma/README.md) - for plasma machines<sup>1</sup>. __NOTE:__ Under development, testers wanted.

* [SD card](../Plugin_SD_card/README.md) - for executing gcode stored on SD card.

* [Spindle](../Plugins_spindle/README.md) - for spindles controlled via MODBUS. __NOTE:__ Not yet verified, testers wanted.

* [Trinamic](../Plugins_motor/README.md) - for Trinamic TMC2130 stepper drivers controlled via SPI or I2C<sup>1</sup>.

* [Laser/PPI](../Plugins_laser/README.md) - for laser machines. __NOTE:__ Under development, testers wanted.

* [Laser/Coolant](../Plugins_laser/README.md) - for laser machines. __NOTE:__ Under development, testers wanted.

<sup>1</sup> Plugin has $-settings, adding or removing it may cause settings for other plugins to be reset to default values.  
<sup>2</sup> Driver support code has $-settings, adding or removing this may cause settings for other plugins to be reset to default values. 

---
2021-02-25
