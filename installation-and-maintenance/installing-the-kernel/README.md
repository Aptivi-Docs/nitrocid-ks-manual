---
icon: compact-disc
description: This page describes about the available methods of installation.
---

# Installing the Kernel

The kernel simulator can be installed on all the supported platforms. The installation steps are straightforward, but must be followed in order to ensure that the kernel starts right.

{% hint style="danger" %}
We don't support starting Nitrocid KS from another environment other than direct execution. If Nitrocid detects that you're running it in such a configuration, functionality will be limited for your security.
{% endhint %}

{% hint style="danger" %}
We no longer support 32-bit platforms; hence we only support ARM64 and AMD64. Find out why [here](https://officialaptivi.wordpress.com/2024/08/03/final-word-regarding-32-bit-support/).
{% endhint %}

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

{% hint style="info" %}
If you've installed a development version of Nitrocid, you may see a warning about such versions. You can, however, hide this warning by opting out of these messages by:

1. Executing the `settings` command
2. Opening the `General` section
3. Enabling the `Development notice acknowledged` option
{% endhint %}

{% hint style="success" %}
It's a good practice to verify that your download is not corrupt using the methods outlined in the [Attestations](https://app.gitbook.com/s/Id4bob6wnHvpX4zbVVtI/csharp-libraries/attestations) page.
{% endhint %}
