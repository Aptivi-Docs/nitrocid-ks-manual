---
description: How to install Nitrocid KS on Windows
---

# 💻 Windows

Installing Nitrocid KS on Windows is pretty easy, but we recommend installing the simulator using the Chocolatey package manager.

Before performing the installation, your Windows system must meet the following requirements:

### KS v0.1.0 or later

To run Nitrocid KS in the absolute minimum requirements, your computer needs to have the following installed:

| System     | Framework                                                          | Terminal                                                  |
| ---------- | ------------------------------------------------------------------ | --------------------------------------------------------- |
| Windows 7+ | [.NET 6.0](https://dotnet.microsoft.com/en-us/download/dotnet/6.0) | [ConEmu](https://conemu.github.io/) or Windows 10 cmd.exe |

However, we recommend that your computer have the below software installed to get the best out of the kernel:

| System      | Framework                                                          | Terminal           |
| ----------- | ------------------------------------------------------------------ | ------------------ |
| Windows 10+ | [.NET 6.0](https://dotnet.microsoft.com/en-us/download/dotnet/6.0) | Windows 10 cmd.exe |

### KS v0.0.24.0 or lower

{% hint style="warning" %}
We support installing KS 0.0.24.0 or lower until **August 2, 2027**.
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
2. Download the latest release RAR file from [this page](https://github.com/Aptivi/Kernel-Simulator/releases). Files that end with the `-dotnet` prefix means that it's for .NET 6.0.
3. Unpack the RAR archive to any folder of your choice
4. Open your favorite terminal emulator, like ConEmu, and change the working directory to a folder containing the Nitrocid KS executable
5. Execute `ks` or `Nitrocid.exe` to start the kernel

## Bleeding-edge

Bleeding-edge builds usually come from building the development branch of the kernel, and they usually contain bugs and other untested features.

If you're a tester to such software, please follow the steps on your Windows machine. Please be sure that you're signed in to your GitHub account.

1. Open [this page](https://github.com/Aptivi/Kernel-Simulator/actions/workflows/build-win.yml)
2. Select the most recent build
3. Scroll down to Artifacts and click on the `ks-build` button to download the ZIP file
4. Extract the file. Be sure that you have the latest version of 7-Zip or your favorite archive manager installed
5. Open your favorite terminal emulator, like ConEmu, and change the working directory to a folder containing the Nitrocid KS executable
6. Execute `ks` or `Nitrocid.exe` to start the kernel
