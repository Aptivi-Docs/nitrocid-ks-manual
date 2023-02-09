---
description: Editing your JSON files using just commands
---

# 🖊 JSON Editor

<figure><img src="../../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

You're looking for an `ed`-like JSON editing experience which allows you to view and edit the JSON file. This is the right place! The `edit` command infers the file type whether it's the text file, the JSON file, or the binary file. It contains many editing tools described in the below section by invoking these commands.

## Commands

These below commands can be used to manipulate with the JSON files:

* `addarray [-parentProperty=prop] <propertyName> <propertyValue1> [propertyValue2] [propertyValue3]...`
  * Adds the array containing the values
* `addproperty [-parentProperty=prop] <propertyName> <propertyValue>`
  * Adds the property containing the value
* `addobject [-parentProperty=prop] <arrayName> <valueInArray>`
  * Adds the object containing the value inside the array
* `clear`
  * Clears the JSON file
* `delproperty <propertyName>`
  * Removes a property from the JSON file
* `exitnosave`
  * Exits the JSON shell without saving the changes
* `jsoninfo`
  * Shows information about the JSON file, including properties for individual JSON objects contained within the file
* `print [property]`
  * Prints either the entire JSON file or a property
* `save [-b|-m]`
  * Saves the JSON file. `-b` is for beautified JSON, and `-m` is for minified JSON
