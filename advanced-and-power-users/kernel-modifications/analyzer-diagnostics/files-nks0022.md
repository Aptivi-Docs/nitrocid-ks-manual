---
description: Use Parsing.GetInvalidPathChars()
---

# 📉 Files - NKS0022

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>Path.GetInvalidPathChars</code> instead of <code>Parsing.GetInvalidPathChars()</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>Parsing.GetInvalidPathChars()</code> instead of <code>Path.GetInvalidPathChars</code></td></tr><tr><td>Description</td><td><code>Parsing.GetInvalidPathChars()</code> always returns invalid characters for Windows paths, regardless of the host operating system, while <code>Path.GetInvalidPathChars</code> returns a list of forbidden path characters for an operating system, which may be wrong in .NET 6.0 or later for the following characters: '"', '&#x3C;', '>'.</td></tr></tbody></table>

### Extended Description

This code analyzer detects the usage of `GetInvalidPathChars` from the standard `Path` class found in the `System.IO` namespace.

**TODO: Populate this section once we finish adding analyzers tracked internally.**

### Analysis Comparison

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

#### Before the fix

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    var invalidChars = Path.GetInvalidPathChars();
</strong>}
</code></pre>

#### After the fix

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    var invalidChars = Parsing.GetInvalidPathChars();
</strong>}
</code></pre>

### Suppression

You can suppress this suggestion by including it in the appropriate place, whichever is convenient.

For more information about how to suppress any warning issued by the Nitrocid analyzer, visit the below page:

{% embed url="https://learn.microsoft.com/en-us/dotnet/fundamentals/code-analysis/suppress-warnings" %}

### Recommendation

We recommend that every caller which use this function use the recommended abovementioned method.
