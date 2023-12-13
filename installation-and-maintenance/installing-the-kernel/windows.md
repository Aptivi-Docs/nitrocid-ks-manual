---
description: How to install Nitrocid KS on Windows
---

# 💻 Windows

<figure><img src="../../.gitbook/assets/Beta3-001-Welcome.png" alt=""><figcaption></figcaption></figure>

Installing Nitrocid KS on Windows is pretty easy, but we recommend installing the simulator using the Chocolatey package manager.

Before performing the installation, your Windows system must meet the following requirements:

{% hint style="info" %}
Extra kernel add-ons may require additional hardware on your computer to work. For example, the BassBoom addon requires that you have audio drivers installed on your computer.
{% endhint %}

### KS v0.1.0 or later

To run Nitrocid KS in the absolute minimum requirements, your computer needs to have the following installed:

| System     | Framework                                                          | Terminal                                                  |
| ---------- | ------------------------------------------------------------------ | --------------------------------------------------------- |
| Windows 7+ | [.NET 8.0](https://dotnet.microsoft.com/en-us/download/dotnet/8.0) | [ConEmu](https://conemu.github.io/) or Windows 10 cmd.exe |

However, we recommend that you have the below software installed on your computer to get the best out of the kernel:

| System      | Framework                                                          | Terminal           |
| ----------- | ------------------------------------------------------------------ | ------------------ |
| Windows 10+ | [.NET 8.0](https://dotnet.microsoft.com/en-us/download/dotnet/8.0) | Windows 10 cmd.exe |

{% hint style="info" %}
If you see the shield icon <img src="../../.gitbook/assets/image.png" alt="" data-size="line"> in the corner of the Nitrocid logo shown in the **Nitrocid.exe** file, don't worry about it; Nitrocid only probes your hard drives with the help of SpecProbe ([see why](../../versions-and-compatibility/compatibility-notes-for-ks-api-revisions/upgrading-to-api-v3.0/from-0.1.0-beta-2-to-0.1.0-beta-3.md#specprobe-updated-to-1.2.0)), nothing else.
{% endhint %}

### KS v0.0.24.0 or lower

{% hint style="warning" %}
We support installing KS 0.0.24.0 or lower until the full deprecation of .NET Framework.
{% endhint %}

To run Nitrocid KS in the absolute minimum requirements, your computer needs to have the following installed:

| System     | Framework                                                                                                        | Terminal                                                  |
| ---------- | ---------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| Windows 7+ | [.NET 6.0](https://dotnet.microsoft.com/en-us/download/dotnet/6.0)                                               | [ConEmu](https://conemu.github.io/) or Windows 10 cmd.exe |
| Windows 7+ | [.NET Framework 4.8](https://dotnet.microsoft.com/en-us/download/dotnet-framework/thank-you/net48-web-installer) | [ConEmu](https://conemu.github.io/) or Windows 10 cmd.exe |

However, we recommend that your computer have the below software installed to get the best out of the kernel:

| System      | Framework                                                                                                        | Terminal           |
| ----------- | ---------------------------------------------------------------------------------------------------------------- | ------------------ |
| Windows 10+ | [.NET 6.0](https://dotnet.microsoft.com/en-us/download/dotnet/6.0)                                               | Windows 10 cmd.exe |
| Windows 10+ | [.NET Framework 4.8](https://dotnet.microsoft.com/en-us/download/dotnet-framework/thank-you/net48-web-installer) | Windows 10 cmd.exe |

## Installation

There are several ways to install Nitrocid KS on Windows systems. We recommend installing KS using the Chocolatey package manager for simplicity.

### Method 1: Chocolatey

This step-by-step guide shows you how to install Nitrocid KS using the package manager, [Chocolatey](https://chocolatey.org/install), assuming that you already have it on your system.

1. Ensure that Chocolatey is installed to your system PATH
2. Open your favorite terminal emulator, like ConEmu, and execute the following command: `choco install ks`
3. Start Nitrocid KS using `ks`

### Method 2: Manual unpack

If you like to manually unpack the Nitrocid KS packages, follow these steps:

1. Ensure that you have all the required software installed
2. Download the latest release ZIP file from [this page](https://github.com/Aptivi/Kernel-Simulator/releases).
3. Unpack the ZIP archive to any folder of your choice using [7-Zip](https://7-zip.org/)
4. Open your favorite terminal emulator, like ConEmu, and change the working directory to a folder containing the Nitrocid KS executable
5. Execute `ks` or `Nitrocid.exe` to start the kernel

{% hint style="info" %}
For 0.0.24.0 or older, files that end with the `-dotnet` prefix means that it's for .NET 6.0.
{% endhint %}

## Bleeding-edge

Bleeding-edge builds usually come from building the development branch of the kernel, and they usually contain bugs and other untested features.

If you're a tester to such software, please follow the steps on your Windows machine. Please be sure that you're signed in to your GitHub account.

1. Open [this page](https://github.com/Aptivi/Kernel-Simulator/actions/workflows/build-win.yml)
2. Select the most recent build
3. Scroll down to Artifacts and click on the `ks-build` button to download the ZIP file
4. Extract the file. Be sure that you have the latest version of 7-Zip or your favorite archive manager installed
5. Open your favorite terminal emulator, like ConEmu, and change the working directory to a folder containing the Nitrocid KS executable
6. Execute `ks` or `Nitrocid.exe` to start the kernel
