---
description: Files and folders are essential for your daily computing usage
---

# 📂 Files and Folders

Files and folders are created to organize your documents, photos, music, videos, and other types of files. They are useful for many purposes, like organizing your archives, your albums, your backups, your personal files, and other types.

Nitrocid KS simulates this component with the help of kernel drivers using your host computer's filesystem to perform common file operations, such as copying, moving, deleting, editing, and many others. In addition, it also supports advanced features, like file content type detection and file lock check.

To see how it works, consult the below page to take you to the inner workings of the Nitrocid kernel filesystem.

{% content-ref url="../../advanced-and-power-users/inner-workings/inner-essentials/nitrocid-filesystem.md" %}
[nitrocid-filesystem.md](../../advanced-and-power-users/inner-workings/inner-essentials/nitrocid-filesystem.md)
{% endcontent-ref %}

### Interactive file manager

<figure><img src="../../.gitbook/assets/Beta3-056-Files.png" alt=""><figcaption></figcaption></figure>

This interactive TUI is a powerful file manager that allows you to view what's inside the folders, as well as performing operations, like copying, moving, or deleting, on files and folders, just like [Total Commander](https://www.ghisler.com/index.htm) or [Midnight Commander](https://midnight-commander.org/).

The file management TUI can be accessed using the `ifm` command. You can use the following keys to manipulate with the files here:

* `Enter`: Go to a folder or open a file
* `F1`: Copy folder or file to the other pane's current working directory
* `F2`: Move a folder or file to the other pane's current working directory
* `F3`: Deletes a file or folder
* `F4`: Goes one directory up
* `F5`: Shows an information box containing file or directory information
* `F6`: Allows you to enter a relative or absolute path to a local folder in the current pane
* `SHIFT + F1`: Allows you to enter a directory to copy the selected file to
* `SHIFT + F2`: Allows you to enter a directory to move the selected file to
* `F9`: Allows you to rename a selected file or folder to another name
* `F10`: Allows you to make a new folder
* `F11`: Gets the file checksum
* `F12`: Verifies the selected file
* `P`: Previews a file in a non-modal informational box
* `Tab`: Switches panes
* `Esc`: Exits the application

{% hint style="info" %}
You can turn on/off the file size display on the status in the kernel settings, but this will affect all other applications that use this settings entry.
{% endhint %}
