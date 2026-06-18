---
description: Changing how the network works
icon: plug-circle-bolt
---

# Network Drivers

The network driver is one of the supported driver types on Nitrocid KS. These drivers allow you to change how the network works, thus earning dynamic network improvements, such as providing better methods to perform network operations.

The network drivers have the following characteristics:

* Interface: `INetworkDriver`
* Base class: `BaseNetworkDriver`

The network drivers have the functions that you can optionally override, and are listed in the relevant API documentation.

The `NetworkDriverTools` class contains tools to get all the network drivers and their names and set a network driver as a default. The driver management tools also allow you to do the same thing, though you'll have to specify the driver type.
