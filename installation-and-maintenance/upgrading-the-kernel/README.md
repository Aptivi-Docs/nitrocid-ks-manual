---
description: This page talks about available methods of upgrading
icon: up
---

# Upgrading the Kernel

{% hint style="warning" %}
### Stop!

Before you can upgrade, you need to consider the following:

* Mods will need to be upgraded to the version that you're upgrading to.
* Configuration backups, including those that are created by your mods, will have to be created before each upgrade.

As for upgrading to 0.1.0, old configuration styles are no longer supported and are kept in your home directory for reference. However, starting from 0.1.0.5, you can migrate most of your old-style configuration (as early as 0.0.16.0 released on 2021) to 0.1.0 and later.
{% endhint %}

Nitrocid KS can be upgraded in all supported platforms. However, some upgrades might break your mods and configuration files, so please be sure that you follow the compatibility notes which is linked below.

{% content-ref url="https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/versions-and-compatibility/compatibility-notes-for-ks-api-revisions/upgrading-to-api-v3.0-series" %}
[Upgrading to API v3.0 series](https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/versions-and-compatibility/compatibility-notes-for-ks-api-revisions/upgrading-to-api-v3.0-series)
{% endcontent-ref %}

Nitrocid KS can be seamlessly updated if you installed Nitrocid through Chocolatey or Windows Installer on Windows systems. For Ubuntu and Arch systems, Nitrocid PPA installs can also be updated through `apt upgrade` and your AUR helper's package upgrade command.

However, if this mechanism fails, you can rely on manually updating. Select your platform to get instructions.

{% content-ref url="windows.md" %}
[windows.md](windows.md)
{% endcontent-ref %}

{% content-ref url="macos.md" %}
[macos.md](macos.md)
{% endcontent-ref %}

{% content-ref url="linux.md" %}
[linux.md](linux.md)
{% endcontent-ref %}

{% content-ref url="android.md" %}
[android.md](android.md)
{% endcontent-ref %}
