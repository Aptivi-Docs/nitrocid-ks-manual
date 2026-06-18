---
description: How do the kernel arguments work? And how do they affect the kernel?
icon: square-sliders
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/inner-workings/inner-essentials/kernel-arguments
---

# Kernel Arguments

<figure><img src="../../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

Kernel Arguments are command-line parameters to the simulator that changes the behavior of the kernel.

The arguments are parsed each time the kernel starts up or gets rebooted. If there are any switches or argument parameters, they'll get parsed using the `ProvidedArgumentsInfo` class.

<details>

<summary>Available arguments</summary>

You can take a look at the available arguments, `--argument`, listed below:

| Argument              | Description                                                                                                 |
| --------------------- | ----------------------------------------------------------------------------------------------------------- |
| `attach`              | Attaches a Visual Studio debugger to the current instance of the kernel (Windows only).                     |
| `quiet`               | Starts the kernel quietly.                                                                                  |
| `maintenance`         | Starts the kernel in maintenance mode which behaves like safe mode but with additional features turned off. |
| `safe`                | Starts the kernel in safe mode which disables all mods.                                                     |
| `testInteractive`     | Opens the interactive test facade selection.                                                                |
| `debug`               | Enables debug mode.                                                                                         |
| `terminaldebug`       | Enables terminal debug mode.                                                                                |
| `reset`               | Wipes all settings and resets the kernel to factory settings                                                |
| `bypasssizedetection` | Bypasses the 80x24 console size detection                                                                   |
| `noaltbuffer`         | Prevents the kernel from using the alternative buffer                                                       |
| `noprebootsplash`     | Prevents the kernel from displaying the pre-boot splash                                                     |
| `lang <lang>`         | Selects a pre-boot environment language                                                                     |
| `verbosepreboot`      | Shows extra pre-boot messages                                                                               |

</details>

{% hint style="info" %}
To learn more about `ProvidedArgumentsInfo`, click on the below link:

[Command-Line Arguments](https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/usage/input-reader/shells/command-line-arguments "mention")
{% endhint %}
