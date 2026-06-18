---
description: This page describes how to manage your kernel mods
icon: wrench
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/kernel-modifications/kernel-modification-management
---

# Managing your Mod

Kernel modification files are stored in the following directories that are found under the kernel configuration directory:

* `KSMods`: Stores all the modifications under the `.dll` extension

***

## <mark style="color:$primary;">Mod finalization</mark>

The mod finalization phase gets executed as soon as the mod parser sees the file as a mod (a `.dll` assembly that implements `IMod` from `Nitrocid.Kernel.Extensions`), with a call to the `FinalizeMods()` function. Here's what it does:

{% stepper %}
{% step %}
#### <mark style="color:$primary;">Verifies the script</mark>

If it sees the script as an instance of `IMod`, it fires the `ModParsed` event
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Adds the path to the assembly lookup path list</mark>

Adds mod dependency path to the assembly lookup path (`KSMods/Deps/Mod-FileVersion/`)
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Checks the API version</mark>

Checks the expected mod API minimum version with the kernel API version to see if there is a mismatch.

* If the checker found that the mod needs a higher API version, the mod parsing fails with the appropriate message.
* If the checker couldn't determine the minimum API version required by the kernel mod, it goes ahead, but with a warning that the mod may fail to start.
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Checks some more properties</mark>

Mod parsing fails if:

* the mod has no name.
* the version is not a SemVer 2.0 compliant version, or if the version is empty.
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Satisfies the mod dependencies</mark>

Satisfies the mod dependencies by loading them as appropriate.
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Runs the startup function</mark>

Calls the `script.StartMod()` function in your script
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Adds the mod</mark>

Adds the mod to the mod manager
{% endstep %}
{% endstepper %}

{% hint style="info" %}
The mod system will automatically unload the target mod's directory for assembly lookup. If, for some reason, this fails, you can manually unload their paths from the lookup using the below function:

```csharp
RemovePathFromAssemblySearchPath(Path);
```
{% endhint %}

***

## <mark style="color:$primary;">Some useful tools</mark>

You can make use of some of the useful tools when dealing with mods.

<details>

<summary>Mod-to-Mod Dependencies</summary>

If you want mods to depend on other mods, you can create a JSON file, called the dependency list file, that holds information about the mod name and the required mod version. The format for the dependency list file should be:

{% code title="Mod-moddeps.json" lineNumbers="true" %}
```json
[
    {
        "name": "Mod2",
        "version": "1.0.0"
    }
]
```
{% endcode %}

The dependencies list file should be saved as the name which satisfies this format: `ModName-moddeps.json`. For example, if your mod, called `ProjectVision`, depends on another mod, called `NitroBoost`, you must create that file called `ProjectVision-moddeps.json` that contains the following contents:

{% code title="ProjectVision-moddeps.json" lineNumbers="true" %}
```json
[
    {
        "name": "NitroBoost",
        "version": "1.2.4"
    }
]
```
{% endcode %}

{% hint style="danger" %}
If one of the mod dependencies failed to load, the mod parser will report a failure for that mod.
{% endhint %}

</details>

<details>

<summary>Mod load priorities</summary>

Important mods, including those that load splashes on boot, get loaded after the configuration files load, so people who use custom splashes in their kernel configuration will actually see their custom splashes when the kernel starts up.

However, for optional mods, they get loaded late so they can load properly. This loading is done by scanning the `KSMods` directory and querying every `.DLL` file with `ParseMod()`.

#### <mark style="color:$primary;">Controlling the priority</mark>

You can control when your mod loads (early or late) by overriding the `AddonType` enumeration to point to one of the correct mod priorities, depending on your mod:

* `Important`
* `Optional`

Important mods get loaded before the kernel configuration loads, while the optional ones get loaded after the hardware gets parsed before the system verification stage.

{% code title="Your mod code" lineNumbers="true" %}
```csharp
override ModLoadPriority LoadPriority =>
    ModLoadPriority.Optional;
```
{% endcode %}

</details>

<details>

<summary>Mod Inter-communication</summary>

In addition to the above mod management tools, Nitrocid KS provides you with tools that allow you to communicate with either the other mods or the other addons that implement their public static functions, fields, or properties.

To get started, follow the two pages below, depending on the type of the communication, to get started:

<a href="inter-mod-communication.md" class="button primary">Inter-Mod Communication</a><a href="inter-addon-communication.md" class="button primary">Inter-Addon Communication</a>

{% hint style="info" %}
Mod management classes require that you use the inter-addon communication being done against the `Nitrocid.Extras.Mods` addon.

For example, to manage blacklisted mods, do this:

```csharp
var modManagerType = InterAddonTools.GetTypeFromAddon(KnownAddons.ExtrasMods, "Nitrocid.Extras.Mods.Modifications.ModManager");
InterAddonTools.ExecuteCustomAddonFunction(KnownAddons.ExtrasMods, "AddModToBlacklist", modManagerType, "MaliciousMod.dll");
var blacklistedMods = (IEnumerable<string>?)InterAddonTools.ExecuteCustomAddonFunction(KnownAddons.ExtrasMods, "GetBlacklistedMods", modManagerType) ?? [];
```
{% endhint %}

</details>
