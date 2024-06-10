---
description: Make your own custom boot style!
---

# 💡 Custom Boot Styles

Directly after GRILO reads the configuration file, GRILO proceeds to call the boot style parser to populate all the customized boot styles. It checks for `.dll` files found under the `GRILO/Styles` directory and parses them as appropriate.

If the `.DLL` file is parsed correctly according to the .NET runtime type, the installer will proceed to check the file for any types implementing the `BaseBootStyle` abstract class.

If found, it adds the custom boot style to the custom boot styles list with the name of the file as the name of the style.

When GRILO attempts to parse the name of your custom boot style, it first finds the base boot styles that exist under GRILO. If it can't be found, it attempts to grab a boot style from the custom boot style list that the parser loaded. If it still can't be found, it uses the default bootloader style.

## Implementing your style

To implement your custom boot style, these steps must be followed:

1. Press `Create a new project` on Visual Studio homepage
2. Find `Class Library` and double-click it
3. Write your mod name, like in our example, `MyFirstMod`.
4. Make sure that .NET 6.0 is used. Press `Create`.
5. Right-click on `Dependencies` -> `Manage NuGet Packages`, find `GRILO.Bootloader`, and install it.
6. Once the package is installed, go to the `Class1.cs` source file
7. Write next to the class file `: BaseBootStyle, IBootStyle` and import the required namespace by `using GRILO.Bootloader.BootStyle;`.
8. Override the necessary methods using the `override` keyword for each one as appropriate.
   * `public override Dictionary<ConsoleKeyInfo, Action<BootAppInfo>> CustomKeys { get; }`
   * `public override string Render()`
   * `public override string RenderHighlight(int chosenBootEntry)`
   * `public override string RenderModalDialog(string content)`
   * `public override string RenderBootingMessage(string chosenBootName)`
   * `public override string RenderBootFailedMessage(string content)`
9. Now, implement everything as you wish. Once you're done, click on the Build menu and select Build Solution.
10. Once the solution is built, open the file explorer to the solution directory by right-clicking on the solution and selecting `Open Folder in File Explorer`.
11. Navigate to the output directory and copy the `.dll` file to `Splashes` under the `%localappdata%/GRILO` folder.
12. Make note of the file name and open the GRILO configuration file, `BootloaderConfig.json`
13. Change the value of `Boot style` to the file name of your custom boot style
14. Start GRILO. Your custom GRILO bootloader style should appear instead of the regular one.

## Key handling

Your custom boot style can make use of the custom key bindings to do custom actions. They can be defined by overriding the `CustomKeys` dictionary with a new dictionary containing the console key and the action with the boot app info passed to it as an argument, like below:

```csharp
public override Dictionary<ConsoleKeyInfo, Action<BootAppInfo>> CustomKeys { get; } = new()
{
    { new ConsoleKeyInfo(...), (bai) => ... }
}
```

If any key other than the `UP ARROW`, `DOWN ARROW`, and `ENTER`, the key handler attempts to parse the key according to the custom key list defined by your boot style. If the key pressed is the same as one of the defined keys, the handler executes the action with the chosen boot application, whose type is `BootAppInfo`, as the argument passed to it.

## Bootloader state

You can also access the bootloader state by referencing the `BootloaderState` class. This class provides you with the following options:

* `WaitingForBootKey`
* `WaitingForFirstBootKey`

This can be used for your custom boot styles to change their behavior, depending on the state.
