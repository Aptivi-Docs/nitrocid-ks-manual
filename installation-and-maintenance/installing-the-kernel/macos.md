---
description: How to install Nitrocid KS on macOS
icon: apple
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/installation-and-maintenance/installing-the-kernel/macos
---

# macOS

Installing Nitrocid KS on macOS is pretty easy. Before performing the installation, your macOS system must meet the following requirements:

{% hint style="info" %}
Extra kernel add-ons may require additional hardware on your computer to work. For example, the BassBoom addon requires that you have audio drivers installed on your computer.
{% endhint %}

To run Nitrocid KS in the absolute minimum requirements, your computer needs to have the following installed:

| System                 | Framework                                                            | Terminal                                       |
| ---------------------- | -------------------------------------------------------------------- | ---------------------------------------------- |
| macOS Sonoma or higher | [.NET 10.0](https://dotnet.microsoft.com/en-us/download/dotnet/10.0) | [iTerm 2.0](https://iterm2.com/downloads.html) |

***

## <mark style="color:$primary;">Installation</mark>

There is one way to install Nitrocid KS on macOS systems. Follow these steps to get started:

{% stepper %}
{% step %}
#### <mark style="color:$primary;">Check your dependencies</mark>

Ensure that you have all the required software installed
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Download the latest ZIP</mark>

Download the latest release ZIP file from [this page](https://github.com/Aptivi/Kernel-Simulator/releases).
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Extract the archive</mark>

Unpack the ZIP archive to any folder of your choice
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Open the terminal emulator</mark>

Open your favorite terminal emulator, like iTerm2, and change the working directory to a folder containing the Nitrocid KS executable
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Execute Nitrocid on your terminal</mark>

Execute `dotnet Nitrocid.dll` to start the kernel
{% endstep %}
{% endstepper %}

***

## <mark style="color:$primary;">Upgrade</mark>

The only way to upgrade Nitrocid in macOS is to unpack the updated files manually. To upgrade, follow these steps:

{% stepper %}
{% step %}
#### <mark style="color:$primary;">Download the latest ZIP</mark>

Download the latest release ZIP file from [this page](https://github.com/Aptivi/Kernel-Simulator/releases).
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Extract the archive</mark>

Unpack the ZIP archive to any folder of your choice
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Open the terminal emulator</mark>

Open your favorite terminal emulator, like iTerm2, and change the working directory to a folder containing the Nitrocid KS executable
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Execute Nitrocid on your terminal</mark>

Execute `dotnet Nitrocid.dll` to start the kernel
{% endstep %}
{% endstepper %}
