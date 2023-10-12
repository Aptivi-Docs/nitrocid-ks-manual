---
description: Let's go deeper into the filesystem functionality!
---

# 🗃 Nitrocid Filesystem

Generally, Nitrocid KS offers the fully-fledged filesystem functionality that allows you to perform filesystem operations ranging from simple to complex, like copying files to checking their lock state. This is done with the assistance of the kernel drivers, which we covered previously in the below page:

{% content-ref url="kernel-drivers.md" %}
[kernel-drivers.md](kernel-drivers.md)
{% endcontent-ref %}

Your mods can access this, too! However, we'll walk you through the Nitrocid filesystem class hierarchy:

* `KS.Files`
  * This is the general filesystem namespace containing security-related checks for the validity and openness of the files, like lock checks, which are found in the `Filesystem` class. It also contains the kernel path querying system, `Paths`.
* `KS.Files.Attributes`
  * This is the namespace responsible for the attribute management for files.
* `KS.Files.Editors`
  * This is the namespace that holds the tools for type-specific text file editing tools
* `KS.Files.Extensions`
  * This is the namespace responsible for the extension management for files.
* `KS.Files.Folders`
  * This is the namespace that specializes with the listing of folders and querying the current directory.
* `KS.Files.Instances`
  * This is the namespace that holds filesystem-related classes.
* `KS.Files.LineEndings`
  * This is the namespace responsible for the management of the line endings for text files.
* `KS.Files.Operations`
  * This is the namespace which houses common filesystem operations, such as making, copying, opening, or deleting files and folders.
* `KS.Files.PathLookup`
  * This is the namespace that is responsible for the management of the path lookup directories for us with the UESH shell.

{% hint style="danger" %}
We advice you not to use `LineEndings` functions on binary files, since they sometimes contain line endings and they may mess with these binary files. Security measures will ensure that these functions throw before any operation is made.
{% endhint %}

{% hint style="warning" %}
For your mods, access to certain filesystem operations require that you consent to accessing your files. This is to ensure increased privacy.
{% endhint %}

{% hint style="info" %}
To learn more about all the available API functions regarding the filesystem, click [here](https://aptivi.github.io/NitrocidKS/api/KS.Files.html).
{% endhint %}

### Path Checks and Lock Checks

Every filesystem operation committed within the `KS.Files` namespace and its functions get their paths checked with the path neutralizer to make a unified version of the path to point to the file relative to either the current path according to the filesystem routine or to the absolute path provided to the neutralizer. This neutralizer is called `Filesystem.NeutralizePath()`.

However, the neutralizer also checks for the validity of the path as a mitigation to the Windows 10 NTFS corruption and forced BSOD bugs by calling the `ThrowOnInvalidPath()` function.

{% hint style="warning" %}
If the conditions were met:

* Attempting to access a Windows path including `$i30`, which is the NTFS volume bitmap, or
* Attempting to open the `kernelconnect` node on `condrv` using a specially crafted path,

The checker will throw a `KernelException` with the `KernelExcceptionType` of `Filesystem` stating that the attempt of accessing these paths is invalid.
{% endhint %}

Optionally, the functions also make use of the file and folder lock checking mechanisms by invoking one of these functions:

* `IsFileLocked()`
* `IsFolderLocked()`
* `IsLocked()`
* `WaitForLockRelease()`
* `WaitForLockReleaseIndefinite()`

Consult the above link to the API reference for more info about how to use these functions to check the lock on your target file.

### Filesystem Entries

`FileSystemEntry` contains necessary information about your file or folder, like checking to see if it exists, determining the type of the entry, and so on.

You can create a new instance of this class, assuming that you've imported the `KS.Files.Instances` namespace, by simply calling the constructor like below:

```csharp
var entry = new FileSystemEntry(pathToFile);
```

{% hint style="info" %}
You don't need to neutralize the path before making a new instance of this class; it'll neutralize your path and you can access both the original and the neutralized paths.
{% endhint %}

### Extension handling

The Nitrocid filesystem provides you with an option to open the files deterministically without opening the hex editor on binary files using the extension handlers. Currently, only the interactive file manager (IFM) uses this feature to open any file.

Handling extensions consists of a class, called `ExtensionHandler`, that contains information about how to open the file ending in a specific extension, and has the following properties:

* `Extension`
  * File extension that is being handled
* `MimeType`
  * MIME type of the extension
* `Handler`
  * A function to execute with the full path to the requested file as the first argument

You can register your custom handler using the `RegisterHandler()` function found in the `ExtensionHandlerTools` class. This way, next time IFM opens up a file with an extension that contains your handler, it will execute your own custom handler.

Additionally, any mod that uses `OpenDeterministically()` on a file will trigger your custom handlers.

{% hint style="warning" %}
Make sure that you unregister all your handlers when unloading your mod. `RegisterHandler()` throws if it discovers that your handler that handles your specific extension is already added to the list of handlers.
{% endhint %}

{% hint style="warning" %}
Currently, we only support one handler per extension, but we're working on removing that limitation soon.
{% endhint %}

### Filesystem read and write

You can read from a file or write to a file using the Nitrocid API to get its contents or write your own content to a file. The file paths are always neutralized to your current working directory, unless you specify a rooted path (absolute path).

The following writing APIs are available:

* `WriteContents()`
  * Useful if you have an array of text
* `WriteContentsText()`
  * Useful if you have a plain text
* `WriteAllLinesNoBlock()`
  * Useful if you have an array of text and want a non-blocking write
* `WriteAllTextNoBlock()`
  * Useful if you have a plain text and want a non-blocking write
* `WriteAllBytes()`
  * Useful for writing binary files

The following reading APIs are available:

* `ReadContents()`
  * Useful if you have a text file and want to parse it line by line
* `ReadContentsText()`
  * Useful if you have a text file and want to parse it as a whole string
* `ReadAllLinesNoBlock()`
  * Useful if you have a text file and want to parse it line by line with a non-blocking read
* `ReadAllTextNoBlock()`
  * Useful if you have a text file and want to parse it as a whole string with a non-blocking read
* `ReadAllBytes()`
  * Useful for reading binary files

### File decode and encode

You can decode and encode files using the below commands:

* `decodefile <file> [algorithm]`
* `encodefile <file> [algorithm]`

Encoded files using the default encoding algorithm are saved to `<file>.encoded`, and the decoded files are saved to the original file name without the `.encoded` prefix.

### File content printing

When you print file contents to the console or render it as a string for preview, you may need to use one of the `FileContentPrinter` functions. However, it depends on your goal:

* If you want to print the file content to the console deterministically, use the `Display*()` functions.
* If you just want to synthesize a string of how it would appear as previewed for different purposes, like previewing a file in an informational box, use the `Render*()` functions.
