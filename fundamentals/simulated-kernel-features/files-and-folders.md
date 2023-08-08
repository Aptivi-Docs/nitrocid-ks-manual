---
description: Files and folders are essential for your daily computing usage
---

# 📂 Files and Folders

Files and folders are created to organize your documents, photos, music, videos, and other types of files. They are useful for many purposes, like organizing your archives, your albums, your backups, your personal files, and other types.

Nitrocid KS simulates this component with the help of kernel drivers using your host computer's filesystem to perform common file operations, such as copying, moving, deleting, editing, and many others. In addition, it also supports advanced features, like file content type detection and file lock check.

To see how it works, consult the below page to take you to the inner workings of the Nitrocid kernel filesystem.

{% content-ref url="../../advanced-and-power-users/inner-workings/nitrocid-filesystem.md" %}
[nitrocid-filesystem.md](../../advanced-and-power-users/inner-workings/nitrocid-filesystem.md)
{% endcontent-ref %}

### Interactive file manager

<figure><img src="../../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

This interactive TUI is a powerful file manager that allows you to view what's inside the folders, as well as performing operations, like copying, moving, or deleting, on files and folders.

It's an interactive TUI application, so the controls are provided here:

* `Enter`: Go to a folder
* `F1`: Copy folder or file to the other pane's current working directory
* `F2`: Move a folder or file to the other pane's current working directory
* `F3`: Deletes a file or folder
* `F4`: Goes one directory up
* `F5`: Shows an information box containing file or directory information
* `F6`: Allows you to enter a relative or absolute path to a local folder in the current pane
* `Tab`: Switches panes
* `Esc`: Exits the application

### Archive shell

You can interact with the archive files by opening the archive shell to point to a file. This can be achieved using the `archive <path>` command.

You can consult the available commands using the `help` command.
