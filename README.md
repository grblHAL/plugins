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

#### I have written a plugin and I want to make it available to grblHAL users

Pull requests for the plugin code itself is not possible as a new repository has to be created and linked to to the different drivers by adding it as a submodule.
You will have to add it to your own github repository and create pull request\(s\) against the core.

__Plugin name:__  

A plugin has to be given an "official" name so that it can be enabled and added to the startup sequence.  
A #define symbol `<NAME>_ENABLE` and a corresponding function `void <name>_init(void)` is required, `<NAME>` and `<name>` is the upper and lower case name of your plugin.  
To add a call to the init function at startup it has to be added to [plugins_init.h](https://github.com/grblHAL/core/blob/master/plugins_init.h) in the _Third party plugin_ section.
Create a pull request for [plugins_init.h](https://github.com/grblHAL/core/blob/master/plugins_init.h) to get it added.  
An example:
```
#if PROBE_RELAY_ENABLE
    extern void probe_relay_init (void);
    probe_relay_init();
#endif
```

To install the plugin the user has to download the code from your repo and copy it to the folder where _driver.c_ is located and add `#define symbol <NAME>_ENABLE 1` somewhere in the drivers _my_machine.h_ file.

__Addional M-codes:__

If your plugin provides additional M-codes these should be documented in the repo readme and the plugin code.
A pull request for getting them added to [gcode.h](https://github.com/grblHAL/core/blob/4a140576a2acf12172ef3532b16b433a07984f71/gcode.h#L199-L226) might be accepted, more likely so if similar in function to those defined by [Marlin](https://marlinfw.org/docs/gcode/M010-M011.html).  
It is also kind of ok to just cast the enum value [in the code](https://github.com/grblHAL/Templates/blob/master/my_plugin/probe%20select/my_plugin.c), however there is a slight risk that it could clash with other plugins - but not too high if similar to those in the Marlin list.

__Additional `$`-settings:__

Setting numbers for your plugin has to be added to [settings.h](https://github.com/grblHAL/core/blob/4a140576a2acf12172ef3532b16b433a07984f71/settings.h#L165) to avoid clashes.
If any is needed [start a discussion](https://github.com/grblHAL/core/discussions) first as I do not yet have a clear idea about how this should be handled, I guess it should be possible to use non-core settings in some cases.

__Notes__:  
The symbol definition may be added to the compiler command line instead, some IDEs allows this from the UI.  
There is no owner of third party plugin names, existing names can be used for alternative implementations as long as they provide similar functionality.  
Implementations should add information about itself in the `$I` report, see one of the [templates](https://github.com/grblHAL/Templates/tree/master/my_plugin) for how this is done.

---

<sup>1</sup> Plugin has `$`-settings, adding or removing it may cause settings for other plugins to be reset to default values.  
<sup>2</sup> Driver support code has `$`-settings, adding or removing this may cause settings for other plugins to be reset to default values. 

---
2021-11-09
