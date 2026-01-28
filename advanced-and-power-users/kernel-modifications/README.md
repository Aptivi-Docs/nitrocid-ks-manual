---
description: What are the Kernel Modifications?
icon: toolbox
---

# Kernel Modifications

Kernel modifications let you extend the kernel functionality to your liking from custom commands to custom kernel applications. It also lets you unleash your console art by letting you make your own screensaver and your own kernel splash screen.

The kernel modifications also let you call the kernel functions and userspace functions, just like what device drivers and user applications in the major operating systems would do, respectively. However, the kernel modifications aren't zero-code solutions, so make sure that you have a bit of C# skills in order to be able to make kernel mods.

{% hint style="warning" %}
You can also use Visual Basic in your mod code, but we recommend that you avoid using it if possible as we no longer support that language.
{% endhint %}

## Best practices

The best practices for making your own kernel mod ensure that your mod becomes friendly in how it handles the kernel and its components. You'll need to use the mod analyzers to ensure that you use APIs that Nitrocid, Terminaux, and other libraries provide to give your users the best experience. You'll need to use APIs provided by Nitrocid if you want to perform different tasks to ensure that your mod respects all kernel configurations.

{% hint style="info" %}
When building mods, you have to do the following:

* Make sure that your mod has a version that is SemVer v2.0 compliant. You can learn more about how to assign that version [here](your-mod.md).
* Make sure that your mod is strongly signed using your own strong name key. You can use [sn.exe](https://learn.microsoft.com/en-us/dotnet/standard/assembly/create-public-private-key-pair) to generate one.
{% endhint %}

As Nitrocid unloads addon and mod assemblies, there can be several cases where unloading fails when Nitrocid shuts down. If your mod fails to unload itself while Nitrocid is shutting down, there can be several factors that might have blocked the unloading process, such as strong references. In this case, you may need to read the official Microsoft documentation about how to troubleshoot such issues.

{% embed url="https://learn.microsoft.com/en-us/dotnet/standard/assembly/unloadability" %}

{% hint style="warning" %}
Modifications that use Newtonsoft.Json or System.Text.Json may fail to unload, depending on how they're used. If you're using JsonConvert to serialize and to deserialize objects to/from JSON, your mod becomes unable to be unloaded. This is because of the way that those two libraries cache types and other objects during the serialization and deserialization process.

Kernel modifications that use kernel configuration to store their own settings may also fail to unload once the registration process completes. This is because the configuration subsystem internally uses JSON serialization and deserialization to read configuration.

This is a known limitation. You can find more information from the below links:

* [https://github.com/dotnet/runtime/issues/13283](https://github.com/dotnet/runtime/issues/13283)
* [https://github.com/JamesNK/Newtonsoft.Json/issues/2414](https://github.com/JamesNK/Newtonsoft.Json/issues/2414)
* [https://github.com/godotengine/godot-proposals/issues/11819](https://github.com/godotengine/godot-proposals/issues/11819)
* [https://github.com/godotengine/godot/issues/78513](https://github.com/godotengine/godot/issues/78513)
{% endhint %}

## Management

Deep explanation of the kernel modification management can be found in the below page:

{% content-ref url="kernel-modification-management/" %}
[kernel-modification-management](kernel-modification-management/)
{% endcontent-ref %}

## Analyzers

You can use the mod analyzers by consulting the page below:

{% content-ref url="analyzer-diagnostics/" %}
[analyzer-diagnostics](analyzer-diagnostics/)
{% endcontent-ref %}

## Building

If you'd like to build your own modifications, that's great! Click on the page below to get started.

{% content-ref url="your-mod.md" %}
[your-mod.md](your-mod.md)
{% endcontent-ref %}
