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
* `KS.Files.Folders`
  * This is the namespace that specializes with the listing of folders and querying the current directory.
* `KS.Files.Interactive`
  * This is the namespace that holds the interactive file manager functions.
* `KS.Files.LineEndings`
  * This is the namespace responsible for the management of the line endings for text files.
* `KS.Files.Operations`
  * This is the namespace which houses common filesystem operations, such as making, copying, opening, or deleting files and folders.
* `KS.Files.PathLookup`
  * This is the namespace that is responsible for the management of the path lookup directories for us with the UESH shell.
* `KS.Files.Print`
  * This is the namespace that allows you to print the contents of the files.
* `KS.Files.Querying`
  * This is the namespace that allows you to parse, query, search, and check for files and folders.
* `KS.Files.Read`
  * This is the namespace that allows you to read the file contents.

{% hint style="danger" %}
We advice you not to use `LineEndings` functions on binary files, since they sometimes contain line endings and they may mess with these binary files. Security measures will ensure that these functions throw before any operation is made.
{% endhint %}

{% hint style="info" %}
To learn more about all the available API functions regarding the filesystem, click [here](https://aptivi.github.io/NitrocidKS/api/KS.Files.html).
{% endhint %}

### Path Checks and Lock Checks

Every filesystem operation committed within the KS.Files namespace and its functions get their paths checked with the path neutralizer to make a unified version of the path to point to the file relative to either the current path according to the filesystem routine or to the absolute path provided to the neutralizer. This neutralizer is called `Filesystem.NeutralizePath()`.

However, the neutralizer also checks for the validity of the path as a mitigation to the Windows 10 NTFS corruption and forced BSOD bugs by calling the `ThrowOnInvalidPath()` function.

{% hint style="warning" %}
If the conditions were met:

* Attempting to access a Windows path including `$i30`, which is the NTFS volume bitmap, or
* Attempting to open the `kernelconnect` node on `condrv` using a specially crafted path,

The checker will throw a `KernelException` with the `KernelExcceptionType` of `Filesystem` stating that the attempt of accessing these paths is invalid.
{% endhint %}

Optionally, the functions also make use of the file lock checking mechanisms by invoking one of these functions:

* `IsFileLocked()`
* `WaitForLockRelease()`
* `WaitForLockReleaseIndefinite()`

Consult the above link to the API reference for more info about how to use these functions to check the lock on your target file.

{% hint style="danger" %}
We currently don't support checking the directory for locking, but we'll implement that soon.
{% endhint %}
