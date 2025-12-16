---
description: Changing how the hardware prober works
icon: plug-circle-bolt
---

# Hardware Prober Drivers

The hardware prober driver is one of the supported driver types on Nitrocid KS. These drivers allow you to change how the hardware prober works, thus earning dynamic hardware prober improvements.

The hardware prober drivers have the following characteristics:

* Interface: `IHardwareProberDriver`
* Base class: `BaseHardwareProberDriver`

The hardware prober drivers have the functions that you can optionally override, and are listed in the relevant API documentation.

The `HardwareProberDriverTools` class contains tools to get all the hardware prober drivers and their names and set a hardware prober driver as a default. The driver management tools also allow you to do the same thing, though you'll have to specify the driver type.
