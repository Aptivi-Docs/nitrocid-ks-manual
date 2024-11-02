---
icon: play
description: Nitrocid live distribution!
---

# Nitrocid LIVE!

Nitrocid LIVE! is a live distribution powered by Windows Preinstallation Environment (WinPE) for [Windows 11 24H2](https://learn.microsoft.com/en-us/windows-hardware/manufacture/desktop/winpe-intro?view=windows-11). This distribution is available for modern PCs running on either AMD64 or ARM64 processors. You can download these distribution ISO images from the release section of the project repository at GitHub:

* `NKS_Live_amd64.iso`: Nitrocid LIVE! for 64-bit processors
* `NKS_Live_arm64.iso`: Nitrocid LIVE! for ARM64 processors

{% hint style="info" %}
After you download these ISO files, we recommend verifying their integrity by following [this tutorial](https://app.gitbook.com/s/Id4bob6wnHvpX4zbVVtI/csharp-libraries/attestations).
{% endhint %}

## Trying Nitrocid KS out

You can either try it out in a virtual machine or in a real computer.

{% hint style="info" %}
Please note that depending on your hardware combination, you may or may not be able to fully utilize Nitrocid KS features. In case of crashes when `wpeinit` is run, you'll need to answer no to the question that asks you if you want to run `wpeinit`.
{% endhint %}

### Virtual machine (QEMU)

To test Nitrocid LIVE! using QEMU, download the emulator either through your official distribution repository or from the [official website](https://www.qemu.org/download/). For Windows, you can either download the pre-built binaries from one source ([32-bit](https://qemu.weilnetz.de/w32/) and [64-bit](https://qemu.weilnetz.de/w64/)) or through [MSYS2](https://packages.msys2.org/base/mingw-w64-qemu).

After installation, write the below command:

```shell-session
$ qemu-system-x86_64.exe -cdrom "/f/Downloads/NKS_Live_amd64.iso" -m 8G -cpu max
```

{% hint style="info" %}
Change the `"/f/Downloads/NKS_Live_amd64.iso"` part to point to the correct directory.
{% endhint %}

If everything is OK, you should be greeted with this:

<figure><img src="../.gitbook/assets/image (88).png" alt=""><figcaption></figcaption></figure>

After this question, you should be able to see Nitrocid KS initializing.

<figure><img src="../.gitbook/assets/image (89).png" alt=""><figcaption></figcaption></figure>

### Virtual machine (VMware)

Once you create a new virtual machine with at least 8 GB RAM, click on `CD/DVD`, and click on `Browse`. Find the ISO file that you've downloaded, and double-click on it.

<figure><img src="../.gitbook/assets/image (87).png" alt=""><figcaption></figcaption></figure>

Afterwards, start the virtual machine. You may need to press ESC in quick succession, then highlight CD-ROM drive and press ENTER. Nitrocid KS live distribution should start.

{% hint style="info" %}
`wpeinit` may crash with blue screen here, so answer N if it crashes.
{% endhint %}

<figure><img src="../.gitbook/assets/Arch Linux-2024-11-02-12-43-07.png" alt=""><figcaption></figcaption></figure>

After this question, you should be able to see Nitrocid KS initializing.

<figure><img src="../.gitbook/assets/Arch Linux-2024-11-02-12-47-55.png" alt=""><figcaption></figcaption></figure>

## Real hardware

In contrast to virtual machines, sometimes testing things, such as Nitrocid LIVE!, in a real hardware is more beneficial than a virtual machine for performance reasons.

### Using USB stick

Using [Rufus](https://rufus.ie/) or any other USB creation tools, you can create a bootable USB stick that consists of Nitrocid LIVE! bootable disc. Here, we are using Rufus to create a bootable Nitrocid LIVE! USB stick.

Open Rufus, then click on Select. Find the downloaded Nitrocid LIVE! ISO file, then double-click it. Rufus should then recognize the ISO file.

<figure><img src="../.gitbook/assets/image (86).png" alt=""><figcaption></figcaption></figure>

Then, choose a partition scheme for the target system:

* GPT: for UEFI
* MBR: for BIOS or CSM

When you're ready, click on `START`, and follow the prompts. Don't disconnect your USB or your computer during this operation, as this involves formatting the USB stick and copying files to it. Once it's done, you can turn on the target computer to a one-time boot mode, selecting your USB stick.

### Using CD-ROM

{% hint style="info" %}
This step applies to computers that can boot from internal or external CD-ROM readers. In case you can't afford a blank CD-ROM or your CD-ROM burner is unreliable, you can use a USB stick, which is cheaper and more efficient.
{% endhint %}

Once the ISO is downloaded, insert a blank CD to your CD-ROM burner. For example, a blank 4.7 GB DVD-RW shows like the below picture in Windows 11's file explorer:

<figure><img src="../.gitbook/assets/image (84).png" alt=""><figcaption></figcaption></figure>

After that, locate the downloaded Nitrocid LIVE! ISO file (usually in the `Downloads` folder), right click it, and select `Burn` (You may need to click on `Show more options` on Windows 11). A window should look like this:

<figure><img src="../.gitbook/assets/image (85).png" alt=""><figcaption></figcaption></figure>

Tick the verify checkbox and press `Burn` once you verify that you're burning the ISO file on a correct burner (in case of multiple burners). It takes 5 minutes and 17 seconds on a verified burn mode, but that depends on your burner's speed and your configured burn speed.

As this disc is bootable, you can restart either your computer or a target computer and initiate a one-time boot sequence, pointing it to your CD-ROM reader.
