---
description: Build the simulator on Android!
icon: android
---

# Building on Android

In Android phones and tablets with Termux installed with proot, you can comfortably build Nitrocid KS using the command line, since it's the most lightweight solution. However, you must have the prerequisites before being able to build KS.

* [.NET 10.0 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/10.0)
* [Termux](https://f-droid.org/en/packages/com.termux/)

### Using the command-line

If you are a hardcore command-line user or if you prefer using the command-line, follow these steps to build Nitrocid KS right from the command line:

1. Open your terminal emulator on your work directory
2. Execute `git clone https://github.com/Aptivi/NitrocidKS.git`
3. Navigate to the cloned repository, `NitrocidKS`
4. Execute `make dbg` for debug builds and `make` for release builds, or `dotnet restore` and `dotnet build`
5. After building is done, run `dotnet run`

{% hint style="info" %}
We recommend that you use `make` to build Nitrocid, since it automatically checks for .NET installation and prepares the environment
{% endhint %}
