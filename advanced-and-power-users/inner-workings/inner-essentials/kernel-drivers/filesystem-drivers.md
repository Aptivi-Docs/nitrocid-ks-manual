---
description: Changing how the filesystem works
icon: plug-circle-bolt
---

# Filesystem Drivers

The filesystem driver is one of the supported driver types on Nitrocid KS. These drivers allow you to change how the filesystem works, thus earning dynamic filesystem improvements, such as providing better workarounds to perform certain console functions, providing code to speed up the console, and much more.

The console drivers have the following characteristics:

* Interface: `IFilesystemDriver`
* Base class: `BaseFilesystemDriver`

The filesystem drivers have the functions that you can optionally override, and are listed in the relevant API documentation.

The `FilesystemDriverTools` class contains tools to get all the filesystem drivers and their names and set a filesystem driver as a default. The driver management tools also allow you to do the same thing, though you'll have to specify the driver type.
