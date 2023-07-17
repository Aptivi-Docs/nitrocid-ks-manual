---
description: How to install Nitrocid KS on macOS
---

# 🍎 macOS

{% hint style="warning" %}
This installation instructions is based on pre-release version of Nitrocid KS, and the system requirements may change during the development.
{% endhint %}

Installing Nitrocid KS on macOS is pretty easy. Before performing the installation, your macOS system must meet the following requirements:

### KS v0.1.0 or later

To run Nitrocid KS in the absolute minimum requirements, your computer needs to have the following installed:

| System                   | Framework                                                          | Terminal                                       |
| ------------------------ | ------------------------------------------------------------------ | ---------------------------------------------- |
| macOS Catalina or higher | [.NET 6.0](https://dotnet.microsoft.com/en-us/download/dotnet/6.0) | [iTerm 2.0](https://iterm2.com/downloads.html) |

### KS v0.0.20.0 or lower

{% hint style="warning" %}
We support installing KS 0.0.20.0 or lower until **2/22/2027**.
{% endhint %}

The above requirements are applied to the 0.0.20.0 version series or lower. The first version to introduce macOS support is 0.0.16.0. However, if possible, use the recent nightly builds of the upcoming version of the kernel.

## Installation

There is one way to install Nitrocid KS on macOS systems.

## Bleeding-edge

Bleeding-edge builds usually come from building the development branch of the kernel, and they usually contain bugs and other untested features.

If you're a tester to such software, please follow the steps on your macOS machine. Please be sure that you're signed in to your GitHub account.

1. Open [this page](https://github.com/Aptivi/Kernel-Simulator/actions/workflows/build-win.yml)
2. Select the most recent build
3. Scroll down to Artifacts and click on the `ks-build` button to download the ZIP file
4. Extract the file. Be sure that you have the latest version of your favorite archive manager installed
5. Open your favorite terminal emulator, like iTerm 2, and change the working directory to a folder containing the Nitrocid KS executable
6. Execute `ks` or `dotnet Nitrocid.dll` to start the kernel