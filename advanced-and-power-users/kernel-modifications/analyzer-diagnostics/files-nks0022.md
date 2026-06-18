---
description: Use Parsing.GetInvalidPathChars()
icon: chart-mixed
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/kernel-modifications/analyzer-diagnostics/files-nks0022
---

# Files - NKS0022

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>Path.GetInvalidPathChars</code> instead of <code>FilesystemTools.GetInvalidPathChars()</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>FilesystemTools.GetInvalidPathChars()</code> instead of <code>Path.GetInvalidPathChars</code></td></tr><tr><td>Description</td><td><code>FilesystemTools.GetInvalidPathChars()</code> always returns invalid characters for Windows paths, regardless of the host operating system, while <code>Path.GetInvalidPathChars</code> returns a list of forbidden path characters for an operating system, which may be wrong in .NET 6.0 or later for the following characters: <code>"</code>, <code>&#x3C;</code>, <code>></code>.</td></tr></tbody></table>

***

## <mark style="color:$primary;">Extended Description</mark>

This code analyzer detects the usage of `GetInvalidPathChars` from the standard `Path` class found in the `System.IO` namespace.

Using `FilesystemTools.GetInvalidPathChars()`, a weirdness has been discovered on Windows systems running .NET 6.0 or later, because that function doesn't consider the three characters: `"`, `<`, and `>` illegal. Therefore, operations can be made to the files or folders on Windows systems with the three characters on them, causing undefined behavior.

A solution to this problem was made with `GetInvalidPathChars()` from Parsing, because it takes care of this pitfall on Windows systems by placing the three characters above to the blacklist.

***

## <mark style="color:$primary;">Analysis Comparison</mark>

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

### <mark style="color:$primary;">Before the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    var invalidChars = Path.GetInvalidPathChars();
</strong>}
</code></pre>

### <mark style="color:$primary;">After the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    var invalidChars = FilesystemTools.GetInvalidPathChars();
</strong>}
</code></pre>
