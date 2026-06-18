---
description: How to install Nitrocid KS on Linux
icon: linux
---

# Linux

<figure><img src="https://github.com/Aptivi-Stable-Docs/nks-manual-0.1.0/blob/main/.gitbook/assets/146-linux.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
<mark style="color:blue;">**We now officially support**</mark> [<mark style="color:blue;">**Arch Linux**</mark>](https://archlinux.org/) <mark style="color:blue;">**as the distro for 64-bit (AMD + Intel and ARM) processors!**</mark>
{% endhint %}

Installing Nitrocid KS on Linux is straightforward, but we recommend installing the simulator using the manual unpack method.

Before performing the installation, your Linux system must meet the following requirements:

{% hint style="info" %}
Extra kernel add-ons may require additional hardware on your computer to work. For example, the BassBoom addon requires that you have audio drivers installed on your computer.
{% endhint %}

To run Nitrocid KS in the absolute minimum requirements, your computer needs to have the following installed:

| System            | Framework                                                          | Terminal                      |
| ----------------- | ------------------------------------------------------------------ | ----------------------------- |
| Supported distros | [.NET 8.0](https://dotnet.microsoft.com/en-us/download/dotnet/8.0) | Konsole, GNOME Terminal, etc. |

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

{% hint style="info" %}
This only applies to Ubuntu and its derivatives. However, we only support the vanilla Ubuntu distribution. <mark style="color:red;">**Don't try this method on**</mark> [<mark style="color:red;">**Debian**</mark>](https://wiki.debian.org/DontBreakDebian#Don.27t_make_a_FrankenDebian)<mark style="color:red;">**.**</mark>
{% endhint %}

If you're running Ubuntu, you can install Nitrocid KS using the Ubuntu PPA. Just follow these steps:

1. Open your terminal emulator and execute the following:
   * `sudo add-apt-repository ppa:eofla/nitrocid`
   * `sudo apt update`
2. Install the `nitrocid` package and follow the instructions (appending the `-XX` suffix to indicate the third mod API version part, such as `25`)
   * `sudo apt install nitrocid-25`
3. Start `ks` (appending the same suffix above, like `ks-25`), or use your app drawer to find `Nitrocid KS` corresponding to your installed mod API version

You can choose between the version series that you want to upgrade in the output of the `apt` command when it prompts you to select one of them, as `nitrocid` is a virtual package.

### Method 3: Arch Linux AUR

{% hint style="info" %}
This only applies to vanilla Arch Linux. We don't officially support Arch's derivatives, such as Manjaro and EndeavourOS.
{% endhint %}

If you're running Arch, you can install Nitrocid KS using the Arch Linux AUR. Just follow these steps:

1. Open your terminal emulator and install your preferred AUR helper. Further steps assume that you have [Yay](https://github.com/Jguer/yay) installed.
2. Install the `nitrocid-25` package and follow the instructions (appending the `-XX` suffix to indicate the third mod API version part, such as `25`)
   * `yay -Sy nitrocid-25`
3. Start `ks` (appending the same suffix above, like `ks-25`), or use your app drawer to find `Nitrocid KS` corresponding to your installed mod API version

You can't install the release version and the cutting-edge (those with the `-git` suffix) version at the same time, since files conflict.
