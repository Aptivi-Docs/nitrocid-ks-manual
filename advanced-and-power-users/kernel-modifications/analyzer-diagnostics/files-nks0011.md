---
description: Use Listing.GetFileSystemEntries()
icon: chart-mixed
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/kernel-modifications/analyzer-diagnostics/files-nks0011
---

# Files - NKS0011

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>Directory.GetFileSystemEntries</code> instead of <code>FilesystemTools.GetFileSystemEntries()</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>FilesystemTools.GetFileSystemEntries()</code> instead of <code>Directory.GetFileSystemEntries</code></td></tr><tr><td>Description</td><td>Alternatively, <code>FilesystemTools.GetFileSystemEntries()</code> returns a list of paths to files or folders with better support for patterns. You can also use <code>GetFilesystemEntriesRegex()</code> for regular expression support.</td></tr></tbody></table>

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
<strong>    string[] files = Directory.GetFileSystemEntries(PathsManagement.AppDataPath);
</strong>}
</code></pre>

### <mark style="color:$primary;">After the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    string[] files = FilesystemTools.GetFileSystemEntries(PathsManagement.AppDataPath);
</strong>}
</code></pre>
