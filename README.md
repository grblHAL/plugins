## grblHAL plugins

grblHAL's HAL interface is based on function pointers that may be used to add functionality without any need to change the core grbl code. They may also be changed on the fly to redirect calls, eg. the SD-card interface utilizes this to temporarily redirect input from the serial stream to the SD card.

NOTE: A plugin needs to be supported by the processor specific driver - as a minimum a initialization call has to be made. 

* [EEPROM](https://github.com/grblHAL/Plugin_EEPROM/) - for non-volatile storage of settings/data on an external EEPROM or FRAM.

* [Encoder](https://github.com/grblHAL/Plugin_encoder/) - for adjusting overrides<sup>1</sup>. Support for jogging is planned.

* [Keypad](https://github.com/grblHAL/Plugin_I2C_keypad/) - for I2C based keypad<sup>1</sup>. Support for jogging etc. [This](https://github.com/terjeio/I2C-interface-for-4x4-keyboard) is an example of an implementation.

* [Networking](https://github.com/grblHAL/Plugin_networking/) - for telnet or websocket communication<sup>2</sup>.

* [Odometer](https://github.com/grblHAL/Plugin_odometer/) - for logging of distances travelled and machining time. __NOTE:__ For review.

* [Plasma/THC](https://github.com/grblHAL/Plugin_plasma/) - for plasma machines<sup>1</sup>. __NOTE:__ Under development, testers wanted.

* [SD card](https://github.com/grblHAL/Plugin_SD_card/) - for executing gcode stored on SD card.

* [Spindle](https://github.com/grblHAL/Plugins_spindle/) - for spindles controlled via MODBUS. __NOTE:__ Not yet verified, testers wanted.

* [Trinamic](https://github.com/grblHAL/Plugins_motor/) - for Trinamic TMC2130 stepper drivers controlled via SPI or I2C<sup>1</sup>.

* [Laser/PPI](https://github.com/grblHAL/Plugins_laser/) - for laser machines. __NOTE:__ Under development, testers wanted.

* [Laser/Coolant](https://github.com/grblHAL/Plugins_laser/) - for laser machines. __NOTE:__ Under development, testers wanted.

* [Fans](https://github.com/grblHAL/Plugin_fans/) - for fan control.

* [Bluetooth](https://github.com/grblHAL/Plugins_Bluetooth/) - for Bluetooth modules used for wireless communication<sup>1</sup>. __NOTE:__ Preview version.

* [WebUI](https://github.com/grblHAL/Plugin_WebUI/) - adds [ESP32-WEBUI](https://github.com/luc-github/ESP3D-webui) support for some networking capable boards and drivers.

#### Third party plugins

* ['Datron like' RGB indicator lights](https://github.com/5ocworkshop/grblhal-rgb-plugin) - by 5ocworkshop.

#### Example and template plugins

A number of example and template plugins can be found [here](https://github.com/grblHAL/Templates/tree/master/my_plugin). Some are usable 'as-is', some not.

---

<sup>1</sup> Plugin has $-settings, adding or removing it may cause settings for other plugins to be reset to default values.  
<sup>2</sup> Driver support code has $-settings, adding or removing this may cause settings for other plugins to be reset to default values. 

---
2021-10-11
