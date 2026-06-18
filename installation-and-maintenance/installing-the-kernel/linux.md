---
description: How to install Nitrocid KS on Linux
icon: linux
---

# Linux

<figure><img src="../../.gitbook/assets/146-linux.png" alt=""><figcaption></figcaption></figure>

Installing Nitrocid KS on Linux is straightforward, but we recommend installing the simulator using the manual unpack method.

Before performing the installation, your Linux system must meet the following requirements:

{% hint style="info" %}
Extra kernel add-ons may require additional hardware on your computer to work. For example, the BassBoom addon requires that you have audio drivers installed on your computer.
{% endhint %}

To run Nitrocid KS in the absolute minimum requirements, your computer needs to have the following installed:

| System            | Framework                                                          | Terminal                      |
| ----------------- | ------------------------------------------------------------------ | ----------------------------- |
| Supported distros | [.NET 8.0](https://dotnet.microsoft.com/en-us/download/dotnet/8.0) | Konsole, GNOME Terminal, etc. |

### Required packages

You can consult the required dependencies here:

{% content-ref url="../dependency-information.md" %}
[dependency-information.md](../dependency-information.md)
{% endcontent-ref %}

## Installation

There are several ways to install Nitrocid KS on Linux systems.

### Method 1: Manual unpack

If you like to manually unpack the Nitrocid KS packages, follow these steps:

1. Ensure that you have all the required software installed
2. Download the latest release ZIP file from [this page](https://github.com/Aptivi/Kernel-Simulator/releases).
3. Unpack the ZIP archive to any folder of your choice
4. Open your favorite terminal emulator, like Konsole, and change the working directory to a folder containing the Nitrocid KS executable
5. Execute `dotnet Nitrocid.dll` to start the kernel

### Method 2: Ubuntu PPA

If you're running Ubuntu, you can install KS using the Ubuntu PPA. Just follow these steps:

1. Open your terminal emulator and execute the following:
   * `sudo add-apt-repository ppa:eofla/kernel-sim`
   * `sudo apt update`
2. Install the `kernel-simulator` package
   * `sudo apt install kernel-simulator`
3. Start `ks` or use your app drawer to find `Nitrocid KS`
