---
description: Use Checking.Rooted()
icon: chart-mixed
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/kernel-modifications/analyzer-diagnostics/files-nks0021
---

# Files - NKS0021

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>Path.IsPathRooted</code> instead of <code>FilesystemTools.Rooted()</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>FilesystemTools.Rooted()</code> instead of <code>Path.IsPathRooted</code></td></tr><tr><td>Description</td><td><code>FilesystemTools.Rooted()</code> uses the filesystem driver to call <code>Path.IsPathRooted</code>.</td></tr></tbody></table>

***

## <mark style="color:$primary;">Extended Description</mark>

This code analyzer detects the usage of `Delete` from the standard `Directory` class found in the `System.IO` namespace.

Using `Path.IsPathRooted()`, it doesn't use any driver to wrap this call, so it calls the built-in `IsPathRooted()` directly.

Alternatively, you can use `FilesystemTools.Rooted()`, which uses the filesystem driver for extensibility.

***

## <mark style="color:$primary;">Analysis Comparison</mark>

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

### <mark style="color:$primary;">Before the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    Path.IsPathRooted("C:/test.txt");
</strong>}
</code></pre>

### <mark style="color:$primary;">After the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    FilesystemTools.Rooted("C:/test.txt");
</strong>}
</code></pre>
