---
description: Use Moving.MoveFileOrDir()
---

# 📉 Files - NKS0015

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>File.Move</code> instead of <code>Moving.MoveFileOrDir()</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>Moving.MoveFileOrDir()</code> instead of <code>File.Move</code></td></tr><tr><td>Description</td><td><code>Moving.MoveFileOrDir()</code> neutralizes the provided path to its absolute correct path, while <code>File.Move</code> operates at the executable directory (<code>Environment.CurrentDirectory</code>), which may not be what you want.</td></tr></tbody></table>

### Extended Description

This code analyzer detects the usage of `Move` from the standard `File` class found in the `System.IO` namespace.

**TODO: Populate this section once we finish adding analyzers tracked internally.**

### Analysis Comparison

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

#### Before the fix

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    File.Move("test.txt", PathsManagement.AppDataPath);
</strong>}
</code></pre>

#### After the fix

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    Moving.MoveFileOrDir("test.txt", PathsManagement.AppDataPath);
</strong>}
</code></pre>

### Suppression

You can suppress this suggestion by including it in the appropriate place, whichever is convenient.

For more information about how to suppress any warning issued by the Nitrocid analyzer, visit the below page:

{% embed url="https://learn.microsoft.com/en-us/dotnet/fundamentals/code-analysis/suppress-warnings" %}

### Recommendation

We recommend that every caller which use this function use the recommended abovementioned method.
