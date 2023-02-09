---
description: Edit your hex files reliably and in bytes
---

# 💾 Hex Editor

<figure><img src="../../../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>

You're looking for an `ed`-like hex editing experience which allows you to view and edit the binary file. This is the right place! The `edit` command infers the file type whether it's the text file, the JSON file, or the binary file. It contains many editing tools described in the below section by invoking these commands.

{% hint style="danger" %}
Unless you know what you're doing with the binary file, editing this in any way will lead to data corruption or data loss in the targeted file.
{% endhint %}

## Commands

These below commands can be used to host the hex editing tools to edit your hex files:

* `addbyte <byte>`
  * Adds a byte at the end of the file
* `addbytes`
  * Adds the bytes at the end of the file
* `clear`
  * Clears the entire binary file
* `delbyte <bytenumber>`
  * Deletes a byte using the byte number
* `delbytes <startbyte> [endbyte]`
  * Deletes the range of bytes from the first byte number to the second byte number or to the end of the file
* `exitnosave`
  * Exits the hex editor without saving changes
* `print [startbyte] [endbyte]`
  * Prints either the entire file, from the first byte number to the end, or from the first byte number to the second one
* `querybyte <byte> [startbyte] [endbyte]`
  * Queries a byte from either the entire file, from the first byte number to the end, or from the first byte number to the second one
* `replace <byte> <replacedbyte>`
  * Replaces a byte with another byte
* `save`
  * Saves the binary file
