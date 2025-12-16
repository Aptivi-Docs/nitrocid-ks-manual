---
description: Changing how the debug logger works
icon: plug-circle-bolt
---

# Debug Logger Drivers

The debug logger driver is one of the supported driver types on Nitrocid KS. These drivers allow you to change how the debug logger works, thus earning dynamic debug logging.

The console drivers have the following characteristics:

* Interface: `IDebugLoggerDriver`
* Base class: `BaseDebugLoggerDriver`

The debug logger drivers have the functions that you can optionally override, and are listed in the relevant API documentation.

The `DebugLoggerDriverTools` class contains tools to get all the debug logger drivers and their names and set a debug logger driver as a default. The driver management tools also allow you to do the same thing, though you'll have to specify the driver type.
