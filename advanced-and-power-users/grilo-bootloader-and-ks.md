---
description: You can boot into Kernel Simulator using GRILO!
---

# 💿 GRILO Bootloader and KS

The GRILO bootloader simulator simulates the theory of the bootloaders and how they work in any device. It allows you to run any bootable .NET assemblies that implement the `IBootable` interface. To learn more about GRILO, visit the link below:

## GRILO and KS

Kernel Simulator can be bootable using the simulated GRILO bootloader. To install the kernel simulator to this bootloader simulator, follow the instructions below to get started. The bootable application installation paths may differ depending on the platform that you run KS on.

1. Download the Kernel Simulator release files from [this site](https://github.com/Aptivi/Kernel-Simulator/releases). Files that end with `-dotnet` are for the .NET 6.0 version.
2. Unpack the downloaded file to one of the paths, depending on the platform. You may need to create the below folders:
   * Windows: `%localappdata%/GRILO/Bootables/ks/`
   * Linux: `~/.config/grilo/Bootables/ks`
3. Start the GRILO bootloader, and choose one of the `Kernel Simulator` options

The kernel should boot up completely.
