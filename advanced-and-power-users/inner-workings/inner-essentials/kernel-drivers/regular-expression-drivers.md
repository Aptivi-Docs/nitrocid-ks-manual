---
description: Changing how the regular expression works
icon: plug-circle-bolt
---

# Regular Expression Drivers

The regular expression driver is one of the supported driver types on Nitrocid KS. These drivers allow you to change how the regular expression works, thus earning dynamic regular expression improvements.

The regular expression drivers have the following characteristics:

* Interface: `IRegexpDriver`
* Base class: `BaseRegexpDriver`

The regular expression drivers have the functions that you can optionally override, and are listed in the relevant API documentation.

The `RegexpDriverTools` class contains tools to get all the regular expression drivers and their names and set a regular expression driver as a default. The driver management tools also allow you to do the same thing, though you'll have to specify the driver type.
