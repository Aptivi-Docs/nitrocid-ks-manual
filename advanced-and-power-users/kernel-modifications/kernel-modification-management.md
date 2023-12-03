---
description: This page describes how to manage your kernel mods
---

# 🔧 Kernel Modification Management

Kernel modification files are stored in the following directories that are found under the kernel configuration directory:

* `KSMods`: Stores all the modifications under the `.dll` extension
* `KSSplashes`: Stores all the kernel splashes under the `.dll` extension

Custom splashes get loaded before the configuration files load, so people who use custom splashes in their kernel configuration will actually see their custom splashes when the kernel starts up.

However, for mods and screensavers, they get loaded late, so they can load properly. This loading is done by scanning the `KSMods` directory and querying every `.DLL` file with `ParseMod()`.

## Mod parsing

The mod finalization phase gets executed as soon as the mod parser sees the file as a mod (a `.dll` assembly that implements `IMod`), with a call to the `FinalizeMods()` function. Here's what it does:

1. If it sees the script as an instance of `IMod`, it fires the `ModParsed` event
2. Adds mod dependency path to the assembly lookup path (`KSMods/Deps/Mod-FileVersion/`)
3. Checks the expected mod API minimum version with the kernel API version to see if there is a mismatch
   * If the checker found that the mod needs a higher API version, the mod parsing fails with the appropriate message
   * If the checker couldn't determine the minimum API version required by the kernel mod, it goes ahead, but with a warning that the mod may fail to start.
4. Checks the mod localization file from the path: `KSMods/Localization/Mod-FileVersion/`
5. If the mod has no name, the mod will be given the name using the file name.
6. Checks the mod for the version and its SemVer 2.0 compliance. **If the version is not a SemVer 2.0 compliant, mod parsing fails.**
7. Satisfies the mod dependencies by loading them as appropriate.
8. Calls the `script.StartMod()` function in your script
9. Adds the mod to the mod manager
10. Checks the manual file `ModFile.manual` for existence and initializes it.

{% hint style="info" %}
The mod system will automatically unload the target mod's directory for assembly lookup. If, for some reason, this fails, you can manually unload their paths from the lookup using the below function:

```csharp
RemovePathFromAssemblySearchPath(Path);
```
{% endhint %}

### Mod Translations

Your mods can now be translated! The mod parser within the kernel also looks for the localization files found under the `KSMods/Localization/Mod-FileVersion/` path. The format is in JSON, and the file name is the same as the three-letter language name. The format is the same as the regular Nitrocid KS localization files embedded as resources. For example, for the French language, the format would look like below:

{% code title="fre.json" lineNumbers="true" %}
```json
{
  "Name": "French",
  "Transliterable": false,
  "Localizations": {
    "Invalid color template {0}": "Modèle de couleur non valide {0}",
    (...)
  }
}
```
{% endcode %}

{% hint style="info" %}
You must use the `mklang` command within Nitrocid, pointing to a directory that contains your language metadata and your `eng.txt` file containing all strings from your mod in order to be able to translate them within the app. When you're done, save your changes by choosing the `Save` option.
{% endhint %}

In the Localizations property, it holds a group of keys and values. The key is an original string extracted from your mod (`"Invalid color template {0}"`) and the value is the translated string (`"Modèle de couleur non valide {0}"`).

When Nitrocid KS detects your localization file, it tries to parse it and adds your translated strings to the `ModInfo` class, which is used by the `Translate` static class to translate your mod strings.

### Mod-to-Mod Dependencies

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

## Splash parsing

The splashes are different, since they get loaded at early stages of the kernel so the configuration system can set the custom splash as the default splash. The kernel basically calls the `LoadSplashes()` function to query all the splash `.dll` files from the `KSSplashes` directory.

The loader attempts to add the splash dependency directory (`KSSplashes/Deps/Splash-FileVersion/`) to the assembly search path list for the splash loader to be able to resolve the splash dependencies, should it depend on one or more of them.

It then extracts the splash instance from the assembly and checks to see if it exists. If it does, it makes a new `SplashInfo` instance holding all the values from the splash instance and adds it to the available splashes list, making it usable for the splash managers to be able to manipulate with it.

## Manual page parsing

At the end of the mod parsing, the manual pages get initialized by the `InitMan()` function, which checks the file extension `.man` and attempts to create a `Manual` class instance.

In turn, this calls the manual checker that parses the entire file. It checks for the following:

* Every manual page starts with the `(*MAN START*)` header
* Every manual page have two fields:
  * `-REVISION:`: Specifies the manual version
  * `-TITLE:`: Specifies the manual page title
* Every manual page must contain one body
  * `-BODY START-` denotes the start of the body
  * `-BODY END-` denotes the end of the body

Optionally, manual pages can contain comments, under the `~~-` prefix. The parser automatically adds comments with the `TODO` constant to the to-do list.

After this is done, the manual page gets added to the available manual pages list, which lets the manual page management functions and the viewer manipulate with the parsed manual instance.

This is an example of a simple manual page file of a mod:

```
(*MAN START*)

-REVISION:1.0
-TITLE:My first mod!

-BODY START-
This is my body!

This is my mod documentation, which hosts the documentation and technical information about what the mod is supposed to do in the kernel.
-BODY END-
```

## Manual page viewer

The manual page viewer can be invoked with the `modmanual` command, which takes an argument that should be a valid kernel mod name.

When this command is executed, the manual page viewer TUI starts by listing all the available manual pages that the mod provides. Then, it shows you a brief description in the second pane, which will most likely tell you to press `Shift + I` to get access to more information.

### Controls

The viewer supports these controls:

* `F1`: Info about the selected manual page
* `Shift + I`: Opens the info box containing your mod manual
* `ESC`: Exits the viewer
