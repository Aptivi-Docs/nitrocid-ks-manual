---
description: How to upgrade Nitrocid KS on Android
---

# 📱 Android

The only way to upgrade your kernel in Android is to unpack the updated kernel files manually. This method also works for bleeding-edge builds, though you have to use unzip instead. To upgrade, follow these steps:

1. Log in to the Ubuntu proot
   * `proot-distro login ubuntu`
2.  Install wget to download the latest release from [this page](https://github.com/Aptivi/Kernel-Simulator/releases).

    * `apt install wget`
    * `wget https://github.com/Aptivi/Kernel-Simulator/releases/download/v0.x.x.x-beta/0.x.x.x-bin.rar`

    _For 0.0.24.0 or older, files that end with the `-dotnet` prefix means that it's for .NET 6.0._
3. Use unrar (from multiverse) to extract the files
   * `unrar 0.x.x.x-bin.rar`
4. Execute `dotnet Nitrocid.dll`
