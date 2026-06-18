---
description: How to install Nitrocid KS on Android
icon: android
---

# Android

<figure><img src="../../.gitbook/assets/147-android.png" alt=""><figcaption></figcaption></figure>

The tricky part is getting Nitrocid KS to run on Android phones and tablets, especially those that run the latest version of Android.

## Installation

To install Nitrocid KS on your phone or tablet, install the following dependencies:

* [Termux](https://termux.dev/en/)
* [Ubuntu PRoot](https://wiki.termux.com/wiki/PRoot#Installing_Linux_distributions)

Ensure that your Android version is compatible with Termux. You need at least 8 GB of free storage and Android 7.0 or higher.

{% hint style="info" %}
To get a better experience with Nitrocid KS on your phone or your tablet, it's advisable to get a phone or a tablet that supports desktop mode ([Samsung DeX](https://insights.samsung.com/2022/08/12/the-beginners-guide-to-samsung-dex-11/) for example) and a Bluetooth mouse and keyboard.
{% endhint %}

### Required packages

You can consult the required dependencies here:

{% content-ref url="../dependency-information.md" %}
[dependency-information.md](../dependency-information.md)
{% endcontent-ref %}

Once you're done, follow the steps:

1. Install Termux
2. Install `proot-distro` using the following command:
   * `pkg install proot-distro`
3. Install the Ubuntu proot
   * `proot-distro install ubuntu`
4. Log in to the Ubuntu proot
   * `proot-distro login ubuntu`
5. Ensure that you've updated the package cache
   * `apt update`
   * `apt dist-upgrade`
6. Install the .NET 8.0 runtime
   * `apt install dotnet-runtime-8.0`
7. Install `wget` to download the latest release from [this page](https://github.com/Aptivi/NitrocidKS/releases).
   * `apt install wget`
   * `wget https://github.com/Aptivi/Nitrocid/releases/download/v0.x.x.x/0.x.x.x-bin.zip`
8. Install `unzip` to extract the files
   * `apt install unzip`
   * `unzip 0.x.x.x-bin.zip`
9. Execute `dotnet Nitrocid.dll`

## Important notes

Here are important notes to consider when trying to run Nitrocid KS on Android:

{% hint style="warning" %}
Trying to run or build Nitrocid KS on an ARM64 Android device (e.g. Android devices with Qualcomm Snapdragon 8 Gen 2 as SoC) with Termux emits two error messages. The first one is:

<pre class="language-shell-session"><code class="lang-shell-session">$ dotnet build
<strong>GC heap initialization failed with error 0x8007000E
</strong><strong>Failed to create CoreCLR, HRESULT: 0x8007000E
</strong></code></pre>

and the second one is:

<pre class="language-shell-session"><code class="lang-shell-session">$ DOTNET_GCHeapHardLimit=1C0000000 dotnet build
(...)
<strong>error MSB6006: "csc.dll" exited with code 139.
</strong><strong>Build FAILED.
</strong></code></pre>

In order to fix the first message, append the below environment variable before each `dotnet build` command like this:

<pre class="language-shell-session"><code class="lang-shell-session"><strong>$ DOTNET_GCHeapHardLimit=1C0000000 dotnet build
</strong></code></pre>

However, to fix the second message, download the fixed version of `proot` using [this link](https://drive.google.com/file/d/1J9euzuGB5w6WGLVNVxTFVnrauTEzISAV/view?usp=sharing) ([mirror if down](https://mega.nz/file/6dYT2YrY#IPKfJRx3Rt8xql1ggyQ95rgEkpDd_vksP02vnnaOPd4)) and run these commands outside the Ubuntu `proot-distro` environment:

<pre class="language-shell-session"><code class="lang-shell-session"><strong># dpkg -i proot_5.1.107-50_aarch64.deb
</strong><strong># apt-mark hold proot
</strong></code></pre>
{% endhint %}
