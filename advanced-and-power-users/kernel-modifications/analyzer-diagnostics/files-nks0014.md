---
description: Use Making.MakeFile()
icon: chart-mixed
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/kernel-modifications/analyzer-diagnostics/files-nks0014
---

# Files - NKS0014

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>File.Create</code> instead of <code>FilesystemTools.MakeFile()</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>FilesystemTools.MakeFile()</code> instead of <code>File.Create</code></td></tr><tr><td>Description</td><td><code>FilesystemTools.MakeFile()</code> neutralizes the provided path to its absolute correct path, while <code>File.Create</code> operates at the executable directory (<code>Environment.CurrentDirectory</code>), which may not be what you want.</td></tr></tbody></table>

***

## <mark style="color:$primary;">Extended Description</mark>

This code analyzer detects the usage of `Create` from the standard `File` class found in the `System.IO` namespace.

Using `File.Create()`, path neutralization doesn't take place to ensure that we have the correct absolute path. This causes some of the filesystem operations to operate on files, which are located in the wrong place, and, therefore, errors throw about a target not being found.

A solution to this problem was made with `MakeFile()`, because it takes care of the absolute paths and tries to reduce this kind of error caused by passing relative directories to the arguments.

***

## <mark style="color:$primary;">Analysis Comparison</mark>

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

### <mark style="color:$primary;">Before the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    File.Create("test.txt");
</strong>}
</code></pre>

### <mark style="color:$primary;">After the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    FilesystemTools.MakeFile("test.txt");
</strong>}
</code></pre>
