---
description: Choose where to go.
icon: hand-back-point-up
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/bootloader/boot-choices
---

# Boot Choices

Nitrocid's internal bootloader simulates the boot choices as in GRUB and LILO. These allow you to select any operating system to boot from in the real-world. The simulated bootloader lets you select any kernel environment to run the main entry point.

The bootloader has several controls, including the custom ones that your boot style can make use of.

***

## <mark style="color:$primary;">Controls</mark>

The general controls that this bootloader makes use of (and are non-overridable) are listed below:

<table><thead><tr><th width="129.33331298828125">Keybinding</th><th>Description</th></tr></thead><tbody><tr><td><code>UP ARROW</code></td><td>Chooses the boot entry above the current selection. If the current selection is the first selection, it'll go to the last entry available.</td></tr><tr><td><code>DOWN ARROW</code></td><td>Chooses the boot entry below the current selection. If the current selection is the last selection, it'll go to the first entry available.</td></tr><tr><td><code>HOME</code></td><td>Goes to the first entry.</td></tr><tr><td><code>END</code></td><td>Goes to the last entry.</td></tr><tr><td><code>SHIFT + H</code></td><td>Shows the help information (lists available controls for both built-in and boot style-defined keybindings).</td></tr><tr><td><code>ENTER</code></td><td>Boots to the selected kernel environment.</td></tr></tbody></table>
