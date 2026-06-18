---
description: What do I need to run Nitrocid?
---

# 📦 Dependency Information

{% hint style="info" %}
Windows users don't need to read this page as Windows provides all the necessary tools to facilitate the work of the kernel and its addons.
{% endhint %}

## For 0.1.0 or higher

In order to run Nitrocid KS on all the system, you must install the essential requirements as shown in the platform-specific installation pages. However, for Linux and Android systems, you must also install the following dependencies to be able to use Nitrocid.

* For Debian and its derivatives (Ubuntu, LMDE, ...)
  * ```sh
    sudo apt install tzdata
    ```
* For Android (Ubuntu PRoot on Termux)
  * ```sh
    sudo apt install libicu72 tzdata
    ```
* For Red Hat Enterprise Linux, Rocky Linux, AlmaLinux, ...
  * ```sh
    sudo dnf install -y epel-release
    sudo dnf install -y libicu tzdata
    ```
* For OpenSUSE
  * ```sh
    sudo zypper install libicu tzdata
    ```
* For Arch Linux and its derivatives (EndeavorOS, ...)
  * ```sh
    sudo pacman -S icu tzdata
    ```
* For Alpine Linux
  * ```sh
    sudo apk add icu icu-libs icu-data-full tzdata
    ```

{% hint style="info" %}
Depending on a distribution and the amount of packages installed in the current system, the download size will be from 30 to 100 MB.

For addons, extra dependencies might be needed to work. For example, the BassBoom addon might need PulseAudio or ALSA working.
{% endhint %}

Dependency information for each package installed in your target system:

* `icu` and its related packages
  * To provide localization information. Needed for the multilingual kernel system.
* `tzdata`
  * To provide time zone information, like listing all available time zones.

In addition to the base kernel requirements, all addons might require additional packages to be installed in your system:

* `pulseaudio, libasound2, ...`
  * To be able to play music using PulseAudio, ALSA, JACK, etc. Used by the BassBoom addon.

## For older Nitrocid versions (0.0.24.x)

If you wish to run Nitrocid 0.0.24.x, you need to install the following dependencies:

* For Debian and its derivatives (Ubuntu, LMDE, ...)
  * ```sh
    sudo apt install inxi libjson-xs-perl
    ```
* For Android (Ubuntu PRoot on Termux)
  * ```sh
    sudo apt install inxi libjson-xs-perl libicu70
    ```
* For Red Hat Enterprise Linux, Rocky Linux, AlmaLinux, ...
  * ```sh
    sudo dnf install -y epel-release
    sudo dnf install -y inxi perl-JSON-XS libicu
    ```
* For OpenSUSE
  * ```sh
    sudo zypper install inxi perl-JSON-XS libicu
    ```
* For Arch Linux and its derivatives (EndeavorOS, ...)
  * ```sh
    sudo pacman -S inxi perl-json-xs icu
    ```
* For Alpine Linux
  * ```sh
    sudo apk add inxi perl-json-xs icu icu-libs icu-data-full
    ```

{% hint style="info" %}
Depending on a distribution and the amount of packages installed in the current system, the download size will be from 30 to 100 MB.
{% endhint %}

{% hint style="info" %}
If you want to run the .NET Framework version of Nitrocid KS on Linux, you'll need to install the complete Mono stack. Depending on the version, you may need to also install the Visual Basic library from Mono.
{% endhint %}
