---
description: Changing how the encoding works
icon: plug-circle-bolt
---

# Encoding Drivers

The encoding driver is one of the supported driver types on Nitrocid KS. These drivers allow you to change how the encoding works, thus earning dynamic encoding based on your selected encoding algorithms.

The console drivers have the following characteristics:

* Interface: `IEncodingDriver` (symmetric) or `IEncodingAsymmetricDriver` (asymmetric)
* Base class: `BaseEncodingDriver` (symmetric) or `BaseEncodingAsymmetricDriver` (asymmetric)

The encoding drivers have the functions that you can optionally override, and are listed in the relevant API documentation.

The `EncodingDriverTools` class contains tools to get all the encoding drivers and their names and set an encoding driver as a default. The driver management tools also allow you to do the same thing, though you'll have to specify the driver type.
