---
description: You can boot into Nitrocid KS using GRILO!
---

# 💿 Bootable Simulation

The GRILO bootloader simulator simulates the theory of the bootloaders and how they work in any device. It allows you to run any bootable .NET assemblies that implement the `IBootable` interface. To learn more about GRILO, visit the link below:

## GRILO and KS

Nitrocid KS can be bootable using the simulated GRILO bootloader. To install Nitrocid KS to this bootloader simulator, follow the instructions below to get started. The bootable application installation paths may differ depending on the platform that you run KS on.

1. Download the Nitrocid KS release files from [this site](https://github.com/Aptivi/Kernel-Simulator/releases).
2.  Unpack the downloaded file to one of the paths, depending on the platform. You may need to create the below folders:

    * Windows: `%localappdata%/GRILO/Bootables/ks/`
    * Linux: `~/.config/grilo/Bootables/ks`

    <figure><img src="../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>
3.  Start the GRILO bootloader (.NET 6.0), and choose one of the `Nitrocid` options\


    <figure><img src="../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

The kernel should boot up completely.
