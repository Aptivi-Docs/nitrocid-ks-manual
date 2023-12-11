---
description: This page talks about available methods of upgrading
---

# ⏫ Upgrading the Kernel

{% hint style="warning" %}
## Stop!

Before you can upgrade, you need to consider the following:

* Mods will need to be upgraded to the version that you're upgrading to.
* Configuration backups, including those that are created by your mods, will have to be created before each upgrade.

As for upgrading to 0.1.0, old configuration styles are no longer supported and are kept in your home directory for reference. See why [here](../../versions-and-compatibility/compatibility-notes-for-ks-api-revisions/upgrading-to-api-v3.0/from-0.1.0-beta-2-to-0.1.0-beta-3.md).
{% endhint %}

Nitrocid KS can be upgraded in all supported platforms. However, some upgrades might break your mods and configuration files, so please be sure that you follow the compatibility notes which is linked below.

{% content-ref url="../../versions-and-compatibility/compatibility-notes-for-ks-api-revisions/" %}
[compatibility-notes-for-ks-api-revisions](../../versions-and-compatibility/compatibility-notes-for-ks-api-revisions/)
{% endcontent-ref %}

Generally, Nitrocid KS can automatically download an update file and, if launched through the built-in launcher for Linux systems, installs the update itself. For Windows systems, it can be seamlessly updated if you installed Nitrocid through Chocolatey. For Ubuntu systems, Nitrocid PPA installs can also be updated through `apt upgrade`.

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
