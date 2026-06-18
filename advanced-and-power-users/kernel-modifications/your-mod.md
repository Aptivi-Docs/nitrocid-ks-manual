---
description: >-
  This page describes how to make your own custom modification using Visual
  Studio.
icon: vial
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/kernel-modifications/your-mod
---

# Building your Mod

You're looking to create a mod for Nitrocid KS! That's great! Make sure that you have Visual Studio installed. Follow the steps to create your first mod.

{% stepper %}
{% step %}
#### <mark style="color:$primary;">Create a new project</mark>

Press `Create a new project` on Visual Studio homepage

<figure><img src="../../.gitbook/assets/image (193) (1).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Create a class library</mark>

Find `Class Library` and double-click it

<figure><img src="../../.gitbook/assets/image (194) (1).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Name your mod</mark>

Write your mod name, like in our example, `MyFirstMod`.

<figure><img src="../../.gitbook/assets/image (195) (1).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Use the supported framework</mark>

Make sure that `.NET 10.0` is used. Press `Create`.

<figure><img src="../../.gitbook/assets/image (196) (1).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Install</mark> <mark style="color:$primary;">`Nitrocid.Base`</mark>

Right-click on `Dependencies` -> `Manage NuGet Packages`, find `Nitrocid.Base`, and install it.

<figure><img src="../../.gitbook/assets/image (197) (1).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
#### Open the class file

Once the package is installed, go to the `Class1.cs` source file

<figure><img src="../../.gitbook/assets/image (198) (1).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Prepare the class</mark>

Write next to the class file `: IMod` and import the required namespace by `using Nitrocid.Base.Kernel.Extensions;`. You should see errors indicating that you have to implement the methods.

<figure><img src="../../.gitbook/assets/image (199) (1).png" alt=""><figcaption></figcaption></figure>

After implementation, you should see:

<figure><img src="../../.gitbook/assets/image (200) (1).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Configure your mod</mark>

Remove all calls to `NotImplementedException`, set the Version property to a SemVer 2.0-compliant version, and set the minimum supported API version.

<figure><img src="../../.gitbook/assets/image (201) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
You can check the API version by executing the Nitrocid executable with `--apiversion`.
{% endhint %}
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Build your mod once done</mark>

Now, implement everything as you wish. Once you're done, follow the steps on how to create a strong name signing key and [sign your mod](https://learn.microsoft.com/en-us/dotnet/standard/assembly/sign-strong-name). Then, click on the `Build` menu and select `Build Solution`.

<figure><img src="../../.gitbook/assets/image (202) (1).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Open the output folder</mark>

Once the solution is built, open the file explorer to the solution directory by right-clicking on the solution and selecting `Open Folder in File Explorer`.

<figure><img src="../../.gitbook/assets/image (203) (1).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Copy the mod</mark>

Navigate to the output directory and copy the `.dll` file to `KSMods` under the `%localappdata%/KS` folder.

<figure><img src="../../.gitbook/assets/image (204) (1).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Test your mod</mark>

Open Nitrocid KS to test your mod. Ensure that `modman list` lists your mod.

<figure><img src="../../.gitbook/assets/image (205) (1).png" alt=""><figcaption></figcaption></figure>
{% endstep %}
{% endstepper %}

{% hint style="info" %}
You will have to turn on kernel modifications from the kernel settings. Navigate to `General > Start kernel modifications on boot` and turn it on.

You can also make use of the [`KSTemplates`](https://github.com/Aptivi/KSTemplates) repository, which can be installed to Visual Studio using the `dotnet new install path/to/KS.Templates.nupkg` command. It installs both C# and Visual Basic templates for your mods.
{% endhint %}

***

## <mark style="color:$primary;">Bleeding-edge builds</mark>

Bleeding-edge NuGet builds are available in our organization's GitHub Package Registry. In order to use such builds, you'll need to consult the <mark style="color:green;">**Installing canary NuGet packages**</mark> section of the below page:

{% content-ref url="https://app.gitbook.com/s/Id4bob6wnHvpX4zbVVtI/csharp-libraries/installation-and-upgrade/installation" %}
[Installation](https://app.gitbook.com/s/Id4bob6wnHvpX4zbVVtI/csharp-libraries/installation-and-upgrade/installation)
{% endcontent-ref %}
