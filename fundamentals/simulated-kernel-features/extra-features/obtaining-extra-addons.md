---
description: How can I get extra addons?
icon: desktop-arrow-down
---

# Obtaining Extra Addons

You can get these extra features, including extra languages, splashes, and screensavers, by either downloading the addons ZIP file from the releases page of the Nitrocid project at GitHub, or by using the `getaddons` command.

{% hint style="info" %}
When downloading addons, consider the following points:

* It's necessary to reboot the kernel for the addons to get loaded.
* The addon pack size is around **100+ MB**, so you need to download it on unmetered networks, such as WiFi. This is to reduce your data fee.
{% endhint %}

### <mark style="color:$primary;">Installing addons manually</mark>

In case the `getaddons` command didn't work properly, you'll have to resort to installing the kernel addons manually. We have packed the addons pack for each release for easy installation. To install the addons manually, follow these steps:

{% stepper %}
{% step %}
#### <mark style="color:$primary;">Download the addons archive</mark>

Download an `-addons.zip` file that corresponds to your kernel version from [this page](https://github.com/Aptivi/NitrocidKS/releases) and open your favorite archive manager.

<figure><img src="../../../.gitbook/assets/161-addonszip.png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Make the addons folder</mark>

Make a new folder under the Nitrocid KS binary folder called `Addons`.

<figure><img src="../../../.gitbook/assets/162-addonszip.png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Extract all addons</mark>

Extract all the folders to the `Addons` folder.

<figure><img src="../../../.gitbook/assets/163-addonszip.png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Verify that the addons start</mark>

Run Nitrocid KS and verify that the addon commands work.
{% endstep %}
{% endstepper %}

***

## <mark style="color:$primary;">What are addons?</mark>

Addons are program extension libraries that extend the functionality of a program. It allows more flexibility because they either provide extra features, change how a specific program function works, or change how they look and feel.

In addition, Nitrocid KS provides an addon system that loads all the kernel addons that are built with the Nitrocid project. Mods are the second kind of kernel addons that have lesser privileges, but can be made easily by you.

The documentation provides you instructions on how to make your own mod (not zero-code!) using the page below:

{% content-ref url="../../../advanced-and-power-users/kernel-modifications/your-mod.md" %}
[your-mod.md](../../../advanced-and-power-users/kernel-modifications/your-mod.md)
{% endcontent-ref %}
