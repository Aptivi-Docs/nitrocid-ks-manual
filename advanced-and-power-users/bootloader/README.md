---
description: What loads your operating system?
---

# 📀 Bootloader

A bootloader is the first computer program that is run after the Basic Input/Output System (BIOS) or the Unified Extensible Firmware Interface (UEFI) phase. It's the computer program that is responsible for booting an operating system.

There are two stages for the bootloader: the first-stage boot loader and the second-stage boot loader. The first-stage boot loader resides in the boot sector, usually found in the first few bytes of your hard drive. However, the second-stage bootloaders are typically stored on the hard drive and are usually loaded by the first-stage ones.

Second-stage bootloaders can be configured to give the user multiple booting choices, which is what major bootloaders, like Windows Boot Manager and GRUB, do.

The integrated bootloader that is found inside the Nitrocid kernel simulates the second-stage bootloader usually found in your computer's hard drive. It simulates the multiple booting choices to allow you to boot to different applications. It also simulates the booting process by executing other kernel environments.

The bootloader interacts with your keyboard to give the users a chance to select their operating system to be booted. In order to learn more about the bootloader, we need to first explain how the kernel environments work.

## Kernel Environments

Kernel environments are classes that are responsible for storing the entry point of the environment, which runs all the necessary features and handles the entire system. They also contain facilities that modify the behavior of the environments by passing arguments to it.

Kernel environments are managed in the `EnvironmentTools` class, and your mod can access it to create your own kernel environment for your purposes. This is useful in certain situations, especially when you want to make a separate interface for kids that contains games and kid-friendly applications.

The base environment is modeled in a way that you need to override the following functions to create your own environment:

* `Name`: The name of your environment that the bootloader shows.
* `EnvironmentEntry`: A delegate to the entry point of your environment.

{% hint style="info" %}
The kernel environment system basically assumes that your entry point code contains a loop that checks to see if neither a reboot nor a shutdown is requested. The base entry point code looks like this (only the relevant part):

```csharp
private static void MainLoop()
{
    while (!PowerManager.RebootRequested && !PowerManager.KernelShutdown)
    {
        (...)
    }
}
```
{% endhint %}

After that, you'll need to create a new instance of your environment and set it as the default environment using `SetEnvironment()`. Optionally, you can set the arguments using the `SetEnvironmentArgs()` function.

## Bootloader Components

The bootloader contains three essential components:

* Boot choices
* Kernel environments
* Boot styles

To learn more about these, you can consult their own pages.
