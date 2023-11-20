---
description: Build the simulator on Android!
---

# 📱 Building on Android

In Android phones and tablets with Termux installed with proot, you can comfortably build Nitrocid KS using the command line, since it's the most lightweight solution. However, you must have the prerequisites before being able to build KS.

* [.NET 8.0 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/8.0)
* [Termux](https://f-droid.org/en/packages/com.termux/)

{% hint style="info" %}
Ubuntu 23.10 Mantic Minotaur users or later can directly download .NET 8.0 SDK from the official Ubuntu repositories without having to import the Microsoft's repositories.

You may need to manually update your Ubuntu proot distribution to either Mantic Minotaur or to Noble Numbat to be able to use .NET 8.0 SDK.
{% endhint %}

{% hint style="warning" %}
Trying to build Nitrocid KS on an ARM64 Android device (e.g. Android devices with Qualcomm Snapdragon 8 Gen 2 as SoC) with Termux emits two error messages. The first one is:

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

However, to fix the second message, download the fixed version of `proot` using [this link](https://drive.google.com/file/d/1J9euzuGB5w6WGLVNVxTFVnrauTEzISAV/view?usp=sharing) ([mirror if down](https://mega.nz/file/6dYT2YrY#IPKfJRx3Rt8xql1ggyQ95rgEkpDd\_vksP02vnnaOPd4)) and run these commands outside the Ubuntu `proot-distro` environment:

<pre class="language-shell-session"><code class="lang-shell-session"><strong># dpkg -i proot_5.1.107-50_aarch64.deb
</strong><strong># apt-mark hold proot
</strong></code></pre>
{% endhint %}

### Using the command-line

If you are a hardcore command-line user or if you prefer using the command-line, follow these steps to build Nitrocid KS right from the command line:

1. Open your terminal emulator on your work directory
2. Execute `git clone https://github.com/Aptivi/NitrocidKS.git`
3. Navigate to the cloned repository, `NitrocidKS`
4. Execute `dotnet restore` and `dotnet build`
5. After building is done, run `dotnet run public/Nitrocid/Nitrocid.csproj`
