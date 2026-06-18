---
description: How to upgrade Nitrocid KS on Linux
icon: linux
---

# Linux

Upgrading the kernel on Linux is simple, depending on the way you've installed the kernel. To upgrade the kernel, choose your preferred method.

## Method 1: Manually unpacking

If you'd like to manually update your kernel to the latest version or to the latest bleeding-edge version, follow these steps:

1. Ensure that you have all the required software installed
2. Download the latest release ZIP file from [this page](https://github.com/Aptivi/Kernel-Simulator/releases).
3. Unpack the ZIP archive to any folder of your choice
4. Open your favorite terminal emulator, like Konsole, and change the working directory to a folder containing the Nitrocid KS executable
5. Execute `dotnet Nitrocid.dll` to start the kernel

## Method 2: Ubuntu PPA

{% hint style="info" %}
This only applies to Ubuntu and its derivatives. However, we only support the vanilla Ubuntu distribution. <mark style="color:red;">**Don't try this method on**</mark> [<mark style="color:red;">**Debian**</mark>](https://wiki.debian.org/DontBreakDebian#Don.27t_make_a_FrankenDebian)<mark style="color:red;">**.**</mark>
{% endhint %}

If you're running Ubuntu, you can update Nitrocid KS using the Ubuntu PPA, assuming that you have the same series installed. Just follow these steps:

1. Open your terminal emulator and execute the following:
   * `sudo apt update`
2. Install the `nitrocid` package and follow the instructions (appending the `-XX` suffix to indicate the third mod API version part, such as `27`)
   * `sudo apt install nitrocid-27`
3. Start `ks` (appending the same suffix above, like `ks-27`), or use your app drawer to find `Nitrocid KS` corresponding to your installed mod API version

You can choose between the version series that you want to upgrade in the output of the `apt` command when it prompts you to select one of them, as `nitrocid` is a virtual package.

## Method 3: Arch Linux AUR

{% hint style="info" %}
This only applies to vanilla Arch Linux. We don't officially support Arch's derivatives, such as Manjaro and EndeavourOS.
{% endhint %}

If you're running Arch, you can install Nitrocid KS using the Arch Linux AUR. Just follow these steps:

1. Open your terminal emulator and install your preferred AUR helper. Further steps assume that you have [Yay](https://github.com/Jguer/yay) installed.
2. Install the `nitrocid` package and follow the instructions (appending the `-XX` suffix to indicate the third mod API version part, such as `27`)
   * `yay -Sy nitrocid-27`
3. Start `ks` (appending the same suffix above, like `ks-27`), or use your app drawer to find `Nitrocid KS` corresponding to your installed mod API version

You can't install the release version and the cutting-edge (those with the `-git` suffix) version at the same time, since files conflict.
