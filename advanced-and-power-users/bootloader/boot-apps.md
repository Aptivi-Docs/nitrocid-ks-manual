---
description: Boot applications and how they work
---

# 💽 Boot Apps

The `IBootable` interface allows GRILO to decide whether the assembly is a bootable application or not. It can be found in a completely separate library called `GRILO.Boot` and is found under the `GRILO.Boot` namespace.

To make your assembly bootable, you must create one class that implements the `IBootable` interface, assuming that you've already imported the required namespace using the `using GRILO.Boot;` statement at the top of the class file:

```csharp
public class MyBootClass : IBootable
```

The three variables are required to be implemented on your boot class as below:

```csharp
public string Title => "";

public bool ShutdownRequested { get; set; }

public void Boot(string[] args)
{
    (...)
}
```

Let's explain these one by one:

* `Title`
  * The title to be shown on the bootloader. This is going to be the second priority over the boot metadata-defined title.
* `ShutdownRequested`
  * Your boot program **SHOULD** implement it as it is and also **SHOULD** set it to `true` at the end of the program if it ensures success.
* `Boot`
  * This function should call the main entry point of the main application class. The arguments variable stores all the arguments passed to it by the metadata file.

## Boot Metadata

Usually a bootable program supported by GRILO contains its own metadata file, `BootMetadata.json`, to store the variables that are optional for booting. This file is required. This metadata file has the following format:

```json
[
    {
        "OverrideTitle": "Title",
        "Arguments": []
    },
    (...)
]
```

You can specify multiple JSON objects for different arguments passed to the target app that we're booting from. Each object found in the metadata file should contain at least two variables:

* `OverrideTitle`
  * The first-priority title is used by the bootloader to display the app as. Omitting the title will fall it back to the title supplied by the boot class.
  * The type of this variable is a **string**
* `Arguments`
  * Arguments to pass to the entry point.
  * The type of this variable is an **array** of **strings**
* `BootFilePath`
  * This specifies an assembly file containing a class that implements `IBootable`. This path is relative to the boot folder found under the `Bootables` folder.
  * The type of this variable is a **string**

For example, Nitrocid KS makes use of the boot metadata file to make it bootable under several modes. One of them is shown in this example:

```json
[
    {
        "OverrideTitle": "Nitrocid 0.1.0",
        "Arguments": [ "noaltbuffer" ]
    }
]
```

{% hint style="warning" %}
By default, GRILO searches every DLL file (for .NET 6.0) or EXE file (for .NET Framework 4.8) to check to see if they are bootable. Most bootable applications should work properly in this case.

If you found that your bootable app is behaving erratically due to this behavior, such as an app that relies on Inxi.NET or any platform-specific library that has its own assembly in the runtimes folder, you can use the `BootFilePath` property to force GRILO to load only this file.

When you force GRILO to only load a specified file in the above property, the resolver will load the correct versions of the runtime-dependent libraries to ensure that your bootable application will work, regardless of the platform.
{% endhint %}

## Boot Parsing

When GRILO starts up, the bootloader scans the bootable apps path, `GRILO/Bootables` (`GRILO/Bootables_DotNetFx` for .NET Framework 4.8 bootable apps), and any additional folders to scan them for any bootable applications found under their respective folders.

Each directory scanned under the bootable application library will be checked for any `.dll` files for .NET 6.0 GRILO or any `.exe` files for .NET Framework 4.8 GRILO.

If GRILO found an assembly that implements the `IBootable` interface as we showed you earlier, it'll do some further parsing, starting from the `BootMetadata.json` found in the respective directory. GRILO then adds the boot app into the list after all the dependencies are loaded to a separate application domain as necessary.

As soon as GRILO shows the boot menu using your custom boot style configured by the bootloader configuration file, the boot menu attempts to display all the bootable applications.
