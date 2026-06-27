---
description: How to install Nitrocid on Windows
icon: windows
---

# Windows

<figure><img src="../../.gitbook/assets/image (316).png" alt=""><figcaption></figcaption></figure>

Installing Nitrocid on Windows is pretty easy, but we recommend installing the simulator using the Chocolatey package manager.

{% hint style="info" %}
Extra kernel add-ons may require additional hardware on your computer to work. For example, the BassBoom addon requires that you have audio drivers installed on your computer.
{% endhint %}

To run Nitrocid in the absolute minimum requirements, your computer needs to have the following installed:

| System      | Framework                                                            | Terminal                                                  |
| ----------- | -------------------------------------------------------------------- | --------------------------------------------------------- |
| Windows 10+ | [.NET 10.0](https://dotnet.microsoft.com/en-us/download/dotnet/10.0) | [ConEmu](https://conemu.github.io/) or Windows 10 cmd.exe |

***

## <mark style="color:$primary;">Installation</mark>

There are several ways to install Nitrocid on Windows systems. We recommend installing it using either the Chocolatey package manager or the Windows installer for simplicity.

<details>

<summary>Method 1: Using WinGet</summary>

This step-by-step guide shows you how to install Nitrocid using the package manager, [WinGet](https://learn.microsoft.com/en-us/windows/package-manager/winget/#install-winget), assuming that you already have it on your system.

1. Ensure that WinGet is installed to your system PATH
2. Open your favorite terminal emulator, like ConEmu, and execute the following command: `winget install --id Aptivi.Nitrocid.0.2.0.x --source winget`
3. Double-click on `Nitrocid` in your desktop.

</details>

<details>

<summary>Method 2: Using Windows Installer</summary>

The Windows Installer method allows you to easily install Nitrocid.

1. Download the latest Windows Installer EXE file from [this page](https://github.com/Aptivi/Kernel-Simulator/releases)
2. Double-click on a single EXE file, and follow the instructions
3. Double-click on `Nitrocid` in your desktop.

{% hint style="info" %}
You can now exclude the Nitrocid addons during installation by changing the appropriate component.
{% endhint %}

</details>

<details>

<summary>Method 3: Using Chocolatey</summary>

{% hint style="info" %}
We are currently unable to push new versions of Nitrocid to Chocolatey due to technical problems, so we have temporarily paused rolling out new packages.
{% endhint %}

This step-by-step guide shows you how to install Nitrocid using the package manager, [Chocolatey](https://chocolatey.org/install), assuming that you already have it on your system.

1. Ensure that Chocolatey is installed to your system PATH
2. Open your favorite terminal emulator, like ConEmu, and execute the following command: `choco install ks`
3. Double-click on `Nitrocid` in your desktop.

</details>

<details>

<summary>Method 4: Manually unpacking</summary>

If you like to manually unpack the Nitrocid packages, follow these steps:

1. Ensure that you have all the required software installed
2. Download the latest release ZIP file from [this page](https://github.com/Aptivi/Kernel-Simulator/releases)
3. Unpack the ZIP archive to any folder of your choice using [7-Zip](https://7-zip.org/)
4. Open your favorite terminal emulator, like ConEmu, and change the working directory to a folder containing the Nitrocid executable
5. Execute `ks` or `Nitrocid.exe` to start the kernel

</details>

***

## <mark style="color:$primary;">Upgrade</mark>

Upgrading Nitrocid on Windows is pretty simple, depending on the way you've installed it. To upgrade it, choose a method.

<details>

<summary>Method 1: Using WinGet</summary>

Any updates to the Nitrocid Chocolatey package can be done using a built-in WinGet command. To update the kernel, follow these steps:

1. Open your favorite terminal emulator, like ConEmu
2. Run `winget upgrade Aptivi.Nitrocid.0.2.0.x`
3. Once the upgrade is done, run Nitrocid like you normally would

</details>

<details>

<summary>Method 2: Using Windows Installer</summary>

You can update Nitrocid using the Windows Installer method.

1. Download the latest Windows Installer EXE file from [this page](https://github.com/Aptivi/Kernel-Simulator/releases)
2. Double-click on the EXE file and follow the instructions
3. Double-click on `Nitrocid` in your desktop.

{% hint style="info" %}
You can now exclude the Nitrocid addons during installation by changing the appropriate component.
{% endhint %}

</details>

<details>

<summary>Method 3: Using Chocolatey</summary>

{% hint style="info" %}
We are currently unable to push new versions of Nitrocid to Chocolatey due to technical problems, so we have temporarily paused rolling out new packages.
{% endhint %}

Any updates to the Nitrocid Chocolatey package can be done using a built-in Chocolatey command. To update the kernel, follow these steps:

1. Open your favorite terminal emulator, like ConEmu
2. Run `choco upgrade ks`
3. Once the upgrade is done, run Nitrocid like you normally would

</details>

<details>

<summary>Method 4: Manually unpacking</summary>

To update the kernel, perform the same steps as in installing Nitrocid. Run the executable to upgrade your kernel configuration files to the latest.

1. Ensure that you have all the required software installed
2. Download the latest release ZIP file from [this page](https://github.com/Aptivi/Kernel-Simulator/releases)
3. Unpack the ZIP archive to any folder of your choice
4. Open your favorite terminal emulator, like ConEmu, and change the working directory to a folder containing the Nitrocid executable
5. Execute `ks` or `Nitrocid.exe` to start the kernel

</details>
