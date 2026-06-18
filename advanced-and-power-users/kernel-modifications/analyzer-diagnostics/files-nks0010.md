---
description: Use Listing.CreateList()
icon: chart-mixed
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/kernel-modifications/analyzer-diagnostics/files-nks0010
---

# Files - NKS0010

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>Directory.GetFileSystemEntries</code> instead of <code>FilesystemTools.CreateList()</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>FilesystemTools.CreateList()</code> instead of <code>Directory.GetFileSystemEntries</code></td></tr><tr><td>Description</td><td><code>FilesystemTools.CreateList()</code> returns a list of <code>FileSystemEntry</code> instances that provides you information about a file, as well as a wrapper to the <code>FileSystemInfo</code> instance for that file.</td></tr></tbody></table>

***

## <mark style="color:$primary;">Extended Description</mark>

This code analyzer detects the usage of `GetFileSystemEntries` from the standard `Directory` class found in the `System.IO` namespace.

The `GetFileSystemEntries()` from the `Directory` class gives you a randomly-sorted list of files and directories, which may not be convenient for TUI applications, such as the interactive TUI.

`CreateList()` takes care of that by sorting directories and files in an alphabetical order by putting the directories first before the files. This way, this listing can then be used for interactive applications.

***

## <mark style="color:$primary;">Analysis Comparison</mark>

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

### <mark style="color:$primary;">Before the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    var files = Directory.GetFileSystemEntries(PathsManagement.AppDataPath);
</strong>}
</code></pre>

### <mark style="color:$primary;">After the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    var files = FilesystemTools.CreateList(PathsManagement.AppDataPath);
</strong>}
</code></pre>
