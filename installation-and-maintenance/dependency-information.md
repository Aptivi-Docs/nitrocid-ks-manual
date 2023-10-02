---
description: What do I need to run Nitrocid?
---

# 📦 Dependency Information

In order to run Nitrocid KS on all the system, you must install the essential requirements as shown in the platform-specific installation pages.

However, for Linux and Android systems, you must also install the following dependencies to be able to use Nitrocid.

* For Debian and its derivatives (Ubuntu, LMDE, ...)
  * ```sh
    sudo apt install inxi libjson-xs-perl tzdata
    ```
* For Android (Ubuntu PRoot on Termux)
  * ```sh
    sudo apt install inxi libjson-xs-perl libicu70 tzdata
    ```
* For Red Hat Enterprise Linux, Rocky Linux, AlmaLinux, ...
  * ```sh
    sudo dnf install -y epel-release
    sudo dnf install -y inxi perl-JSON-XS libicu tzdata
    ```
* For OpenSUSE
  * ```sh
    sudo zypper install inxi perl-JSON-XS libicu tzdata
    ```
* For Arch Linux and its derivatives (EndeavorOS, ...)
  * ```sh
    sudo pacman -S inxi perl-json-xs icu tzdata
    ```
* For Alpine Linux
  * ```sh
    sudo apk add inxi perl-json-xs icu icu-libs icu-data-full tzdata
    ```

{% hint style="info" %}
Depending on a distribution and the amount of packages installed in the current system, the download size will be from 30 to 100 MB.

For addons, extra dependencies might be needed to work. For example, the BassBoom addon might need PulseAudio or ALSA working.
{% endhint %}

Dependency information for each package installed in your target system:

* `inxi`
  * For probing hardware information. Used by the Inxi.NET library.
* `perl-json-xs (libjson-xs-perl)`
  * To facilitate JSON output of Inxi hardware info. Used by the Inxi.NET library.
* `icu` and its related packages
  * To provide localization information. Needed for the multilingual kernel system.
* `tzdata`
  * To provide time zone information, like listing all available time zones.
