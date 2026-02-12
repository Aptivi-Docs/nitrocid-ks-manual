---
description: This page describes about the available methods of installation or upgrade.
icon: compact-disc
---

# Installation and Upgrade

The kernel simulator can be installed or upgraded on all the supported platforms. The installation or upgrade steps are straightforward, but must be followed in order to ensure that the kernel starts right.

{% hint style="danger" %}
We don't support starting Nitrocid KS from another environment other than direct execution. If Nitrocid detects that you're running it in such a configuration, functionality will be limited for your security.
{% endhint %}

{% hint style="danger" %}
We no longer support 32-bit platforms; hence we only support ARM64 and AMD64. Find out why [here](https://officialaptivi.wordpress.com/2024/08/03/final-word-regarding-32-bit-support/).
{% endhint %}

{% hint style="success" %}
It's a good practice to verify that your download is not corrupt using the methods outlined in the [Attestations](https://app.gitbook.com/s/Id4bob6wnHvpX4zbVVtI/csharp-libraries/attestations) page.
{% endhint %}

***

## <mark style="color:$primary;">Select platform</mark>

Depending on your platform, the amount of disk space taken by KS and its runtime dependencies might vary. Select your platform below and follow the steps.

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

***

## <mark style="color:$primary;">Important considerations for upgrades</mark>

{% hint style="warning" %}
## Stop!

Before you can upgrade, you need to consider the following:

* Mods will need to be upgraded to the version that you're upgrading to.
* Configuration backups, including those that are created by your mods, will have to be created before each upgrade.

As for upgrading to 0.1.0, old configuration styles are no longer supported and are kept in your home directory for reference. However, starting from 0.1.0.5, you can migrate most of your old-style configuration (as early as 0.0.16.0 released on 2021) to 0.1.0 and later. See why [here](../../versions-and-compatibility/compatibility-notes-for-ks-api-revisions/upgrading-to-api-v3.0-series/from-0.1.0-beta-2-to-0.1.0-beta-3.md).

As for upgrading to 0.2.0, you'll need to edit the speed dial entries manually to align with the latest JSON format. Find out [here](../../fundamentals/simulated-kernel-features/extra-features/more-networking/#speed-dial-for-networked-shells).
{% endhint %}

Nitrocid KS can be upgraded in all supported platforms. However, some upgrades might break your mods and configuration files, so please be sure that you follow the compatibility notes which is linked below.

{% content-ref url="../../versions-and-compatibility/compatibility-notes-for-ks-api-revisions/" %}
[compatibility-notes-for-ks-api-revisions](../../versions-and-compatibility/compatibility-notes-for-ks-api-revisions/)
{% endcontent-ref %}
