---
description: Choose where to go.
---

# 📀 Boot Choices

GRILO simulates the boot choices as in GRUB and LILO. These allow you to select any operating system to boot from in the real-world. GRILO lets you select any bootable .NET application to run the main entry point.

The bootloader has several of the controls, including the custom ones that your boot style can make use of.

## Controls

The general controls that GRILO makes use of (and are non-overridable) are listed below:

* `UP ARROW`: Chooses the boot entry above the current selection. If the current selection is the first selection, it'll go to the last entry available.
* `DOWN ARROW`: Chooses the boot entry below the current selection. If the current selection is the last selection, it'll go to the first entry available.
* `HOME`: Goes to the first entry
* `END`: Goes to the last entry
* `SHIFT + H`: Shows the help information (lists available controls for both GRILO and boot style-defined keybindings)
* `ENTER`: Boots to the selected bootable application.
