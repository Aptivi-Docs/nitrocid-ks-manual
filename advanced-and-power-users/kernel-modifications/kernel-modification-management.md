---
description: This page describes how to manage your kernel mods
---

# 🔧 Kernel Modification Management

Kernel modification files are stored in the following directories that are found under the kernel configuration directory:

* `KSMods`: Stores all the modifications under the `.dll` extension
* `KSScreensavers`: Stores all the custom screensavers under the `.dll` extension
* `KSSplashes`: Stores all the kernel splashes under the `.dll` extension

Custom splashes get loaded before the configuration files load, so people who use custom splashes in their kernel configuration will actually see their custom splashes when the kernel starts up.

However, for mods and screensavers, they get loaded late, so they can load properly. This loading is done by scanning the `KSMods` and the `KSScreensavers` directory and querying every `.DLL` file with `ParseMod()` and `ParseCustomSavers()`.

## Mod parsing

The mod finalization phase gets executed as soon as the mod parser sees the file as a mod (a `.dll` assembly that implements `IScript`), with a call to the `FinalizeMods()` function. Here's what it does:

1. If it sees the script as an instance of `IScript`, it fires the `ModParsed` event
2. Adds mod dependency path to the assembly lookup path (`KSMods/Deps/Mod-FileVersion/`)
3. Checks the expected mod API minimum version with the kernel API version to see if there is a mismatch
   * If the checker found that the mod needs a higher API version, the mod parsing fails with the appropriate message
   * If the checker couldn't determine the minimum API version required by the kernel mod, it goes ahead, but with a warning that the mod may fail to start.
4. Calls the `script.StartMod()` function in your script
5. Checks for the mod part name. **If there is no name, the mod parsing fails.**
6. Checks for the mod commands. **If there is a command info entry with an empty command, the mod parsing fails.**
7. If the mod has no name, the mod will be given the name using the file name.
8. Checks for conflicts of the mod part names.
9. Adds the mod part to the parts list with the mod part instance
10. Checks the mod for the version.
11. Checks the mod commands for any conflict with the existing shell commands and resolves it.
12. Checks to see if a command can be added to the shell command list and adds it.
13. Checks the manual file `ModFile.manual` for existence and initializes it.

## Screensaver parsing

If the screensavers parser started, `ParseCustomSavers` gets called, traversing through all the contents of the `KSScreensavers` directory. For each `.dll` file that got detected by this parser, `ParseCustomSaver` gets called, causing this to happen:

1. Tries to get the screensaver instance, `IScreensaver`, from the assembly
2. If the screensaver is valid, it gets information about the screensaver from the instance
3. It adds the screensaver to the custom screensaver list

Once this is successfully done, the screensaver management tools will be able to see the custom screensaver.

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

The manual page viewer can be invoked with the `modmanual` command, which takes either an argument that contains the manual page title for a mod or a `-list` switch that lists all the available manual pages.

Invocation of the command starts with `ViewPage()` getting involved. It starts with printing the manual page information style to the bottom of the console. The text then gets rendered to the memory according to the console width.

The viewer then prints the manual page line to the console with the VT sequence enabled with the help of the presentation system.

### Controls

The viewer supports these controls:

* `ENTER`: Advances to the next page
* `ESC`: Exits the viewer
