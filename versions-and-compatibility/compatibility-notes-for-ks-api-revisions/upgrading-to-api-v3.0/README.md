---
description: Follow the compatibility notes when upgrading your mods to API v3.0
---

# 🔼 Upgrading to API v3.0

As API v3.0 is still in development, the breaking changes get committed and land here. They describe what broke and what should be used instead.

{% hint style="danger" %}
## Critically important notices

When upgrading your mods to API v3.0, consider these:

* Starting from 0.1.0, old configuration styles are no longer supported and are kept in your home directory for reference. The kernel will start from scratch as if you've started it for the first time. Don't worry; all your configuration from 0.0.24.0 are still saved in your home directory. This is because of configuration system changes that happened between 0.0.24.0 and 0.1.0.
* .NET Framework 4.8 is **no longer supported** as of 0.1.0 Beta 1. Please consider using .NET 8.0 instead to continue using Nitrocid KS. This is to improve multi-platform support without having to go to one environment (`dotnetfx` on Windows and `mono` on Linux and macOS) for each platform.
* Starting from API version `3.0.25.353`, Nitrocid KS **requires** elevated permission to run. This means that you may see the shield icon <img src="../../../.gitbook/assets/image.png" alt="" data-size="line"> in the corner of the Nitrocid logo. See why [here](from-0.1.0-beta-2-to-0.1.0-beta-3.md#specprobe-updated-to-1.2.0).
* Starting from API version `3.0.25.361`, mods are no longer organized with mod parts. This feature has been removed and won't be coming back. See why [here](from-0.1.0-beta-2-to-0.1.0-beta-3.md#removed-mod-parts).
{% endhint %}

## To 0.1.0

This version is a futuristic magic that brings in many feature additions and spectacular improvements in all fields, including cosmetic changes.

{% content-ref url="../../version-release-notes/v0.1.x.x-series/" %}
[v0.1.x.x-series](../../version-release-notes/v0.1.x.x-series/)
{% endcontent-ref %}

{% hint style="info" %}
## **Important notices**

When upgrading your mods to API v3.0, consider these:

* A breaking change has been made so that every mod that need to work with API version `3.0.25.123` or higher should satisfy the following conditions for their versions:
  1. Mod versions should satisfy the SemVer v2.0 specification. Mod parsing will fail if an invalid version expression is entered.
* Additionally, a breaking change has been made starting from API version `3.0.25.154` that will make the mod loader fail under the following conditions:
  1. The mod is not strongly signed using any strong naming key and loading untrusted mods is disabled.
* Starting from API version `3.0.25.310`, Nitrocid KS now uses .NET 8.0, which means that all your mods will have to be updated to continue working.
{% endhint %}

This will be populated as soon as we reach the release candidate stage of 0.1.0 to maintain consistency.
