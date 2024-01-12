# Getting Started
To get started, make sure you have a copy of the QGroundControl repository. If you are using a custom build already, you can skip to the next step [here](Logo.md). QGroundControl can be cloned from here:

 - [QGroundControl](https://github.com/mavlink/qgroundcontrol)

Once that is cloned and you can build the project, we are ready to get started on customizations.

If you need to install QGroundControl, the documentation can be found here [https://docs.qgroundcontrol.com/master/en/qgc-dev-guide/getting_started/](https://docs.qgroundcontrol.com/master/en/qgc-dev-guide/getting_started/)

## Custom Builds

*If you are using a pre-existing build, you must **clean** your build directory first.*

 1. Start by renaming the `custom-example` directory to `custom`.
 2. Next, change to the renamed `custom` directory.
 3. Run `python updateqrc.py`.
 4. Build QGC.

This should build successfully, and if we run it, our new customizations will be applied.

**You can switch from *Indoor* or *Outdoor* mode from the settings under *Miscellaneous* in the Color Scheme drop down** 
 - Indoor mode is Dark Mode
 - Outdoor mode is Light Mode

---
[Next: Color Scheme](ColorScheme.md) \
[Prev: ReadMe](Readme.md)
