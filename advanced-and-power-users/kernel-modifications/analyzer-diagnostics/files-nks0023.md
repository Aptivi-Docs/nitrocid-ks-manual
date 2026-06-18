---
description: Use Filesystem.NeutralizePath()
icon: chart-mixed
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/kernel-modifications/analyzer-diagnostics/files-nks0023
---

# Files - NKS0023

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>Path.GetFullPath</code> instead of <code>Filesystem.NeutralizePath()</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>Filesystem.NeutralizePath()</code> instead of <code>Path.GetFullPath</code></td></tr><tr><td>Description</td><td><code>Filesystem.NeutralizePath()</code> neutralizes the provided path to its absolute correct path, but also gives a path separated by the platform-agnostic path separator.</td></tr></tbody></table>

***

## <mark style="color:$primary;">Extended Description</mark>

This code analyzer detects the usage of `GetFullPath` from the standard `Path` class found in the `System.IO` namespace.

While `Path.GetFullPath()` operates on the executable project directory, it doesn't represent the state of the current working directory because the UESH shell doesn't use the built-in current working directory property.

`NeutralizePath()` had to be made to not only solve this problem, but also gives you a unified path that has folder names spearated by the platform-agnostic path separator.

***

## <mark style="color:$primary;">Analysis Comparison</mark>

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

### <mark style="color:$primary;">Before the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    string path = Path.GetFullPath("test.txt");
</strong>}
</code></pre>

### <mark style="color:$primary;">After the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    string path = FilesystemTools.NeutralizePath("test.txt");
</strong>}
</code></pre>
