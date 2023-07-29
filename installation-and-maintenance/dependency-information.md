---
description: What do I need to run Nitrocid?
---

# 📦 Dependency Information

In order to run Nitrocid KS on all the system, you must install the essential requirements as shown in the platform-specific installation pages.

However, for Linux and Android systems, you must also install the following dependencies to be able to use Nitrocid.

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
