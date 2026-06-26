---
description: Changing how the encryption works
icon: plug-circle-bolt
---

# Encryption Drivers

The encryption driver is one of the supported driver types on Nitrocid KS. These drivers allow you to change how the encryption works, thus earning dynamic encryption improvements.

The console drivers have the following characteristics:

* Interface: `IEncryptionDriver`
* Base class: `BaseEncryptionDriver`

The encryption drivers have the functions that you can optionally override, and are listed in the relevant API documentation.

The `EncryptionDriverTools` class contains tools to get all the encryption drivers and their names and set a encryption driver as a default. The driver management tools also allow you to do the same thing, though you'll have to specify the driver type.

{% hint style="warning" %}
Nitrocid supplies the extra encryption drivers using the kernel addons, but some of them require your system to be running below:

* `SHA256Enhanced` (Windows 11 24H2 or later, Linux with OpenSSH 1.1.1 or later, macOS not supported)
* `SHA384Enhanced` (Windows 11 24H2 or later, Linux with OpenSSH 1.1.1 or later, macOS not supported)
* `SHA512Enhanced` (Windows 11 24H2 or later, Linux with OpenSSH 1.1.1 or later, macOS not supported)
{% endhint %}
