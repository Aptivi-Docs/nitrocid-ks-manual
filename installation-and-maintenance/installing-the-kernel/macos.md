---
description: How to install Nitrocid KS on macOS
icon: apple
---

# macOS

Installing Nitrocid KS on macOS is pretty easy. Before performing the installation, your macOS system must meet the following requirements:

{% hint style="info" %}
Extra kernel add-ons may require additional hardware on your computer to work. For example, the BassBoom addon requires that you have audio drivers installed on your computer.
{% endhint %}

To run Nitrocid KS in the absolute minimum requirements, your computer needs to have the following installed:

| System                   | Framework                                                          | Terminal                                       |
| ------------------------ | ------------------------------------------------------------------ | ---------------------------------------------- |
| macOS Catalina or higher | [.NET 8.0](https://dotnet.microsoft.com/en-us/download/dotnet/8.0) | [iTerm 2.0](https://iterm2.com/downloads.html) |

## Installation

There is one way to install Nitrocid KS on macOS systems. Follow these steps to get started:

1. Ensure that you have all the required software installed
2. Download the latest release ZIP file from [this page](https://github.com/Aptivi/Kernel-Simulator/releases).
3. Unpack the ZIP archive to any folder of your choice
4. Open your favorite terminal emulator, like iTerm2, and change the working directory to a folder containing the Nitrocid KS executable
5. Execute `dotnet Nitrocid.dll` to start the kernel
