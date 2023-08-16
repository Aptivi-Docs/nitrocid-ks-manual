---
description: Sometimes we need to check your platform.
---

# 🖥 Kernel Platform

Sometimes, your mod may contain code that only works on certain platforms. For example, your mod may intentionally call an external unmanaged library's function to do something not normally done in the .NET world using P/Invokes. However, native libraries need to be compiled for the target machines.

Or, you may want to change the behavior of your mod by platform or by how the kernel is started, such as if the kernel was started by the GRILO bootloader.

`KernelPlatform` provides functions to detect platforms and environments. This is to make such tasks relatively easy.

{% hint style="warning" %}
Currently, `KernelPlatform` doesn't support checking for architectures, like `IsAmd64()`.
{% endhint %}

## Operating systems

This class provides the following OS-related functions:

* `IsOnWindows()`: Checks to see if Nitrocid KS is running on Windows.
* `IsOnUnix()`: Checks to see if Nitrocid KS is running on Unix and its derivatives, such as Linux, macOS, etc.
* `IsOnMacOS()`: Checks to see if Nitrocid KS is running on Darwin Kernel, the kernel behind macOS.

## Terminals

This class provides the following terminal-related functions:

* `GetTerminalEmulator()`: Gets the terminal emulator name. This may not be accurate.
* `GetTerminalType()`: Gets the terminal type name, such as xterm. This may not be accurate.

{% hint style="warning" %}
There are some terminal emulators advertising themselves as XTerm compliant, but actually aren't fully compliant. We advice that you introduce extra checks to ensure that your terminal emulator fully supports the features that you want to use, especially when it comes with the VT sequences.
{% endhint %}

## Environments

This class provides the following environment-related functions:

* `IsRunningFromGrilo()`: Checks to see whether Nitrocid KS is run from GRILO
* `IsRunningFromTmux()`: Checks to see whether Nitrocid KS is run on TMUX

## CoreCLR

This class provides the following CoreCLR-related functions:

* GetCurrentRid(): Gets the current runtime identifier.

{% hint style="warning" %}
[As of .NET 8.0](https://learn.microsoft.com/en-us/dotnet/core/compatibility/deployment/8.0/rid-asset-list), the above function will return generic runtime identifiers, like win-x64, linux-x64, and so on.

We advice you that you don't rely on it in your mods until we migrate to .NET 8.0. Just use this value for informational purposes only.
{% endhint %}
