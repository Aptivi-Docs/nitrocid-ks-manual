---
description: Let's go deeper into the filesystem functionality!
icon: cabinet-filing
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/inner-workings/inner-essentials/nitrocid-filesystem
---

# Nitrocid Filesystem

<figure><img src="../../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

Generally, Nitrocid KS offers the fully-fledged filesystem functionality that allows you to perform filesystem operations ranging from simple to complex, like copying files to checking their lock state. This is done with the assistance of the kernel drivers, which we covered previously in the below page:

{% content-ref url="kernel-drivers/" %}
[kernel-drivers](kernel-drivers/)
{% endcontent-ref %}

***

## <mark style="color:$primary;">Available namespaces</mark>

Your mods can access this, too! The filesystem part of the kernel contain the following namespaces:

<table><thead><tr><th width="255.33331298828125">Namespace</th><th>Description</th></tr></thead><tbody><tr><td><code>Nitrocid.Files</code></td><td>This is the general filesystem namespace containing all filesystem operations and security-related checks for the validity and openness of the files, like lock checks, which are found in the <code>FilesystemTools</code> class.</td></tr><tr><td><code>Nitrocid.Files.Editors</code></td><td>This is the namespace that holds the tools for type-specific text file editing tools.</td></tr><tr><td><code>Nitrocid.Files.Extensions</code></td><td>This is the namespace responsible for the extension management for files.</td></tr><tr><td><code>Nitrocid.Files.Folders</code></td><td>This is the namespace that contains sorting-related enumerations.</td></tr><tr><td><code>Nitrocid.Files.Instances</code></td><td>This is the namespace that holds filesystem-related classes.</td></tr><tr><td><code>Nitrocid.Files.LineEndings</code></td><td>This is the namespace that holds newline-related enumerations.</td></tr><tr><td><code>Nitrocid.Files.Paths</code></td><td>This is the namespace that is responsible for the management of the kernel path system and the path lookup system.</td></tr></tbody></table>

{% hint style="danger" %}
We advice you not to use `LineEndings` functions on binary files, since they sometimes contain line endings and they may mess with these binary files. Security measures will ensure that these functions throw before any operation is made.
{% endhint %}

{% hint style="warning" %}
For your mods, access to certain filesystem operations require that you consent to accessing your files. This is to ensure increased privacy.
{% endhint %}

***

## <mark style="color:$primary;">Available tools</mark>

In the filesystem part of Nitrocid, here are the available tools:

<details>

<summary>Path Checks and Lock Checks</summary>

Every filesystem operation committed within the `Nitrocid.Files` namespace and its functions get their paths checked with the path neutralizer to make a unified version of the path to point to the file relative to either the current path according to the filesystem routine or to the absolute path provided to the neutralizer. This neutralizer is called `Filesystem.NeutralizePath()`.

Optionally, the functions also make use of the file and folder lock checking mechanisms by invoking one of these functions:

* `IsFileLocked()`
* `IsFolderLocked()`
* `IsLocked()`
* `WaitForLockRelease()`
* `WaitForLockReleaseIndefinite()`

</details>

<details>

<summary>Filesystem Entries</summary>

`FileSystemEntry` contains necessary information about your file or folder, like checking to see if it exists, determining the type of the entry, and so on.

#### <mark style="color:$primary;">Base entry properties</mark>

These are the information currently available, but you can obtain more information using the `BaseEntry` property:

<table><thead><tr><th width="199.66668701171875">Property</th><th>Description</th></tr></thead><tbody><tr><td><code>Exists</code></td><td>Checks to see if the file or directory exists.</td></tr><tr><td><code>Type</code></td><td>The type of the filesystem entry. This is only populated once.</td></tr><tr><td><code>OriginalFilePath</code></td><td>The original file path that was passed to the constructor.</td></tr><tr><td><code>FilePath</code></td><td>The neutralized file path.</td></tr><tr><td><code>FileSize</code></td><td>The file size. This property's value is <code>-1</code> if the entry is a directory or non-existent.</td></tr><tr><td><code>BaseEntryUnprocessed</code></td><td>The base entry from the unprocessed file path.</td></tr><tr><td><code>BaseEntry</code></td><td>The base entry from the neutralized file path.</td></tr></tbody></table>

#### <mark style="color:$primary;">Creating a new file system entry class instance</mark>

You can create a new instance of this class, assuming that you've imported the `Nitrocid.Files.Instances` namespace, by simply calling the constructor like below:

```csharp
var entry = new FileSystemEntry(pathToFile);
```

{% hint style="info" %}
You don't need to neutralize the path before making a new instance of this class; it'll neutralize your path and you can access both the original and the neutralized paths.
{% endhint %}

</details>

<details>

<summary>Extension handling</summary>

The Nitrocid filesystem provides you with an option to open the files deterministically without opening the hex editor on binary files using the extension handlers. Currently, only the interactive file manager (IFM) uses this feature to open any file.

#### <mark style="color:$primary;">Properties of the handler</mark>

Handling extensions consists of a class, called `ExtensionHandler`, that contains information about how to open the file ending in a specific extension, and has the following properties:

<table><thead><tr><th width="129">Property</th><th>Description</th></tr></thead><tbody><tr><td><code>Extension</code></td><td>File extension that is being handled</td></tr><tr><td><code>MimeType</code></td><td>MIME type of the extension</td></tr><tr><td><code>Implementer</code></td><td>The extension handler implementer name (can also be used as a codename for the handler)</td></tr><tr><td><code>Handler</code></td><td>A function to execute with the full path to the requested file as the first argument</td></tr><tr><td><code>InfoHandler</code></td><td>A function get information from a file and render said information to a string instance</td></tr></tbody></table>

#### <mark style="color:$primary;">Registering a custom handler</mark>

You can register your custom handler using the `RegisterHandler()` function found in the `ExtensionHandlerTools` class. This way, next time IFM opens up a file with an extension that contains your handler, it will execute your own custom handler.

```csharp
ExtensionHandlerTools.RegisterHandler(".txt", "txthandler", (path) => Opening.OpenEditor(path, true), (path) => $"Lines: {File.ReadAllLines(path).Length}");
```

#### <mark style="color:$primary;">Triggering custom handler</mark>

Additionally, any mod that uses `OpenDeterministically()` on a file will trigger your custom handlers.

{% hint style="warning" %}
Make sure that you unregister all your handlers when unloading your mod. `RegisterHandler()` throws if it discovers that your handler that handles your specific extension is already added to the list of handlers.

```csharp
var handler = ExtensionHandlerTools.GetExtensionHandler(".txt", "txthandler");
ExtensionHandlerTools.UnregisterHandler(".txt", handler);
```
{% endhint %}

#### <mark style="color:$primary;">Saving defaults</mark>

For the list of default handlers, they get saved to the `ExtensionHandlers.json` file. These handlers get used everytime a request to `GetExtensionHandler(string extension)` function is made.

</details>

<details>

<summary>Filesystem read and write</summary>

You can read from a file or write to a file using the Nitrocid API to get its contents or write your own content to a file. The file paths are always neutralized to your current working directory, unless you specify a rooted path (absolute path).

#### <mark style="color:$primary;">Writing to files</mark>

The following writing APIs are available:

| Function                 | Description                                                        |
| ------------------------ | ------------------------------------------------------------------ |
| `WriteContents()`        | Useful if you have an array of text.                               |
| `WriteContentsText()`    | Useful if you have a plain text.                                   |
| `WriteAllLinesNoBlock()` | Useful if you have an array of text and want a non-blocking write. |
| `WriteAllTextNoBlock()`  | Useful if you have a plain text and want a non-blocking write.     |
| `WriteAllBytes()`        | Useful for writing binary files.                                   |

#### <mark style="color:$primary;">Reading from files</mark>

The following reading APIs are available:

| Function                | Description                                                                                     |
| ----------------------- | ----------------------------------------------------------------------------------------------- |
| `ReadContents()`        | Useful if you have a text file and want to parse it line by line.                               |
| `ReadContentsText()`    | Useful if you have a text file and want to parse it as a whole string.                          |
| `ReadAllLinesNoBlock()` | Useful if you have a text file and want to parse it line by line with a non-blocking read.      |
| `ReadAllTextNoBlock()`  | Useful if you have a text file and want to parse it as a whole string with a non-blocking read. |
| `ReadAllBytes()`        | Useful for reading binary files.                                                                |

</details>

<details>

<summary>File decode and encode</summary>

You can decode and encode files using the below commands:

* `decodefile <file> [algorithm]`
* `encodefile <file> [algorithm]`

Encoded files using the default encoding algorithm are saved to `<file>.encoded`, and the decoded files are saved to the original file name without the `.encoded` prefix.

</details>

<details>

<summary>File content printing</summary>

When you print file contents to the console or render it as a string for preview, you may need to use one of the `FileContentPrinter` functions. However, it depends on your goal:

* If you want to print the file content to the console deterministically, use the `Display*()` functions.
* If you just want to synthesize a string of how it would appear as previewed for different purposes, like previewing a file in an informational box, use the `Render*()` functions.

</details>

<details>

<summary>MIME Metadata</summary>

Additionally, the `Extensions` part of the filesystem feature contains a mechanism that allows you to manipulate with the MIME metadata.

* You can get the MIME type from an extension using the `GetMimeType()` function.

{% hint style="info" %}
The supported MIME types are available [here](https://github.com/Aptivi/NitrocidKS/commit/c4a52ae47ebc870adb72d11b6a2a641db95684d7#diff-4591e343dac43550e94f94b4cfe0f51e2189301ea58219ef5f3efc05caab0cc7R31).
{% endhint %}

</details>

<details>

<summary>Symbolic Links (a.k.a. Shortcuts)</summary>

Symbolic links are shortcuts to a single file or directory that simplify the path to the target file or folder. They are useful for many purposes.

To make a symbolic link, you can use the `MakeSymlink()` function and its `Try` counterpart from the `Making` class from the `Operations` namespace. This function takes two arguments:

* The link name specifies a path to the symbolic link. This name must not exist.
* The link target specifies a path to an existent file or folder.

</details>

<details>

<summary>Kernel paths</summary>

The `Nitrocid.Files.Paths` namespace contains a group of functions that allow you to use the pre-defined kernel paths and custom paths. The pre-defined kernel paths can be get by either getting a value from its associated property, such as `AddonsPath`, or by using the `GetKernelPath()` function.

```csharp
public static string GetKernelPath(KernelPathType PathType) { }
```

#### <mark style="color:$primary;">Registration of custom paths</mark>

The custom paths can be registered and unregistered by using the functions that are outlined below:

```csharp
public static void RegisterKernelPath(string pathType, string path) { }
public static void UnregisterKernelPath(string pathType) { }
```

If you want to define your own custom path, you must register the kernel path with a file or folder that you choose. It's not necessarily a file or a folder that exists, since you may create it in your mod.

#### <mark style="color:$primary;">Usage of custom paths</mark>

After the registration, you can use the `GetKernelPath()` function to give it a name of your registered path type.

```csharp
public static string GetKernelPath(string PathType) { }
```

</details>

<details>

<summary>Copying and Moving</summary>

Filesystem APIs in Nitrocid provide copying and moving files and/or directories.

#### <mark style="color:$primary;">Copying and moving modes</mark>

The base filesystem driver implements three copying and moving modes.

<mark style="color:$primary;">**Copying and moving a source file to a destination**</mark>

```csharp
// Copying
public static void CopyFile(string Source, string Destination) { }
public static bool TryCopyFile(string Source, string Destination) { }

// Moving
public static void MoveFile(string Source, string Destination) { }
public static bool TryMoveFile(string Source, string Destination) { }
```

<mark style="color:$primary;">**Copying and moving a source directory to a destination**</mark>

```csharp
// Copying
public static void CopyDirectory(string Source, string Destination) { }
public static void CopyDirectory(string Source, string Destination, bool ShowProgress) { }
public static bool TryCopyDirectory(string Source, string Destination) { }
public static bool TryCopyDirectory(string Source, string Destination, bool ShowProgress) { }

// Moving
public static void MoveDirectory(string Source, string Destination) { }
public static void MoveDirectory(string Source, string Destination, bool ShowProgress) { }
public static bool TryMoveDirectory(string Source, string Destination) { }
public static bool TryMoveDirectory(string Source, string Destination, bool ShowProgress) { }
```

<mark style="color:$primary;">**Copying and moving a source file or directory to a destination**</mark>

```csharp
// Copying
public static void CopyFileOrDir(string Source, string Destination) { }
public static bool TryCopyFileOrDir(string Source, string Destination) { }

// Moving
public static void MoveFileOrDir(string Source, string Destination) { }
public static bool TryMoveFileOrDir(string Source, string Destination) { }
```

#### <mark style="color:$primary;">Operation</mark>

When copying or moving a file or directory, the functions first check for the source to check to see if it's a file, a directory, or both, depending on the function used. For example, if you're copying a directory to a destination, you can use either `CopyFileOrDir()` or `CopyDirectory()`, but not `CopyFile()`.

The `TryCopy*()` and the `TryMove*()` functions return `true` if copying or moving is successful, and false if the operation failed. The normal `Copy*()` and the `Move*()` functions throw an exception if any failure occurs.

</details>

***

## <mark style="color:$primary;">File and Folder Selector</mark>

<figure><img src="../../../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

The file manager includes two separate TUIs that allow you to select a file or a folder conveniently. We'll explain what do the two selectors do and how they work.

<details>

<summary>File Selector</summary>

When it comes to file selection, there is a function dedicated to opening the file selector effortlessly, called `SelectFile()`, which you can find its two signatures below:

{% code title="Selection.cs" lineNumbers="true" %}
```csharp
public static string SelectFile() { }
public static string SelectFile(string path) { }
```
{% endcode %}

When the selector is open, you can do almost all the things, just like in the normal file management TUI, but with some of the features removed, such as copying and moving to the secondary pane.

To select a file, you can press `Enter` to select it. Then, you'll have to exit it manually to save the selected file, thus making `SelectedFile` return a selected file.

</details>

<details>

<summary>Files Selector</summary>

Like the file selector, but it also allows you to select more than one file to allow your mod to perform various operations on these files, such as bulk copying the selected files to a single target directory.

There is a function that allows you to use this kind of selector, called `SelectFiles()`.

{% code title="Selection.cs" lineNumbers="true" %}
```csharp
public static string[] SelectFiles() { }
public static string[] SelectFiles(string path) { }
```
{% endcode %}

To select a file, press `Enter` to select it. Once you're done selecting various files, you'll have to exit it manually to save the selected files, thus making `SelectedFiles` return a list of selected files.

</details>

<details>

<summary>Folder Selector</summary>

When the folder selector is open using the `SelectFolder()` function, you can select a folder effortlessly by pressing the spacebar on the target directory highlighted.

{% code title="Selection.cs" lineNumbers="true" %}
```csharp
public static string SelectFolder() { }
public static string SelectFolder(string path) { }
```
{% endcode %}

After that, you can press `Esc` to save the selected folder and pass it to the application, which it can access the selected folder value using the `SelectedFolder` property.

</details>

<details>

<summary>Folders Selector</summary>

Like the folder selector, but it also allows you to select more than one folder to allow your mod to perform various operations on these folders, such as bulk copying the selected folders to a single target directory.

There is a function that allows you to use this kind of selector, called `SelectFolders()`.

{% code title="Selection.cs" lineNumbers="true" %}
```csharp
public static string[] SelectFolders() { }
public static string[] SelectFolders(string path) { }
```
{% endcode %}

To select a file, press `Space` to select it. Once you're done selecting various folders, you'll have to exit it manually to save the selected folders, thus making `SelectedFolders` return a list of selected folders.

</details>
