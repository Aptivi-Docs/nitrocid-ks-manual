---
description: How to upgrade Nitrocid KS on Windows
icon: windows
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/jTBo3FZPtPjlFHZkVmzr/installation-and-maintenance/upgrading-the-kernel/windows
---

# Windows

Upgrading your kernel on Windows is pretty simple, depending on the way you've installed the simulator. To upgrade your kernel, choose a method. Please note that the second method, which is unpacking the update yourself, can also be done with the bleeding-edge builds.

{% hint style="info" %}
If you're upgrading bleeding-edge builds, it's recommended that you uninstall the old copy and reinstall the newer version. It doesn't wipe your Nitrocid KS data, though.
{% endhint %}

## Method 1: Using WinGet

Any updates to the Nitrocid Chocolatey package can be done using a built-in WinGet command. To update the kernel, follow these steps:

1. Open your favorite terminal emulator, like ConEmu
2. Run `winget upgrade Aptivi.Nitrocid.0.1.0.x`
3. Once the upgrade is done, run Nitrocid like you normally would

## Method 2: Windows Installer

The Windows Installer method allows you to easily upgrade Nitrocid.

1. Download the latest Windows Installer EXE file from [this page](https://github.com/Aptivi/Kernel-Simulator/releases)
2. Double-click on a single EXE file, and follow the instructions
3. Double-click on `Nitrocid` in your desktop.

{% hint style="info" %}
You can now exclude the Nitrocid addons during installation by changing the appropriate component.
{% endhint %}

## Method 3: Using Chocolatey

{% hint style="info" %}
We are currently unable to push new versions of Nitrocid to Chocolatey due to technical problems, so we have temporarily paused rolling out new packages.
{% endhint %}

Any updates to the Nitrocid Chocolatey package can be done using a built-in Chocolatey command. To update the kernel, follow these steps:

1. Open your favorite terminal emulator, like ConEmu
2. Run `choco upgrade ks`
3. Double-click on `Nitrocid` in your desktop.

## Method 4: Manually unpacking

To update the kernel, perform the same steps as in installing. Run the executable to upgrade your kernel configuration files to the latest.

1. Ensure that you have all the required software installed
2. Download the latest release ZIP file from [this page](https://github.com/Aptivi/Kernel-Simulator/releases).
3. Unpack the ZIP archive to any folder of your choice
4. Open your favorite terminal emulator, like ConEmu, and change the working directory to a folder containing the Nitrocid executable
5. Execute `ks` or `Nitrocid.exe` to start the kernel
