---
description: Follow the compatibility notes when upgrading your mods to API v4.1 series
icon: up
---

# Upgrading to API v4.1 series

As API v4.1 is still in development, the breaking changes get committed and land here. They describe what broke and what should be used instead.

***

## <mark style="color:$primary;">From 0.2.0.6 to 0.2.1</mark> <a href="#from-0.0.24-to-0.1.0" id="from-0.0.24-to-0.1.0"></a>

This version introduces many changes to the kernel API to make it easier to use than never before. It also deprecates and removes APIs that are no longer necessary, while introducing new features that make it easier for you to create useful kernel modifications.

### <mark style="color:$primary;">Detailed important changes</mark> <a href="#detailed-important-changes-2" id="detailed-important-changes-2"></a>

This section explains how to adapt the important changes to your mod code so that it works with 0.2.0 and higher. This highlights the most important changes that we have compiled for you.

<details>

<summary>Removed all SpecProbe wrappers</summary>

SpecProbe wrappers were implemented in `KernelPlatform` before getting moved to SpecProbe so that more applications were able to use them outside Nitrocid. As a result, we've removed all SpecProbe wrappers.

The following functions were removed as of 0.2.1 Tech Preview:

* `IsOnWindows()`
* `IsOnUnix()`
* `IsOnUnixMusl()`
* `IsOnMacOS()`
* `IsOnAndroid()`
* `GetTerminalEmulator()`
* `GetTerminalType()`
* `IsRunningFromTmux()`
* `IsRunningFromScreen()`
* `GetCurrentGenericRid()`

We will probably move more SpecProbe wrappers as we introduce different versions for different .NET frameworks in a future version of SpecProbe expected around July 2026.

</details>
