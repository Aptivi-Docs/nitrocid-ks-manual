---
description: Use TextTools.SplitNewLines()
icon: chart-mixed
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/kernel-modifications/analyzer-diagnostics/text-nks0055
---

# Text - NKS0055

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>TextTools.SplitNewLinesOld()</code> instead of <code>TextTools.SplitNewLines()</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>TextTools.SplitNewLines()</code> instead of <code>TextTools.SplitNewLinesOld()</code></td></tr><tr><td>Description</td><td><code>TextTools.SplitNewLines()</code> is able to correctly split text with Mac OS 9 newline characters and mixed new line characters, while <code>TextTools.SplitNewLinesOld()</code> can't split such strings properly.</td></tr></tbody></table>

***

## <mark style="color:$primary;">Extended Description</mark>

This code analyzer detects the usage of `SplitNewLinesOld()` from the `TextTools` class found in the `KS.Misc.Text` namespace.

While `SplitNewLinesOld()` is here to split the new lines efficiently, there has been problems dealing with the mixed newline handling, especially when it comes to splitting text by the Mac OS 9 newline, which is a carriage return character `\r`.

As a result, `SplitNewLines()` has been rewritten to more efficiently handle these situations.

***

## <mark style="color:$primary;">Analysis Comparison</mark>

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

### <mark style="color:$primary;">Before the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
    string var = "Hello\nWorld!";
<strong>    var split = var.SplitNewLinesOld();
</strong>}
</code></pre>

### <mark style="color:$primary;">After the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
    string var = "Hello\nWorld!";
<strong>    var split = var.SplitNewLines();
</strong>}
</code></pre>

### <mark style="color:$primary;">After the fix (alternate)</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code" data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
    string var = "Hello\nWorld!";
<strong>    var split = var.SplitNewLinesOld();
</strong>}
</code></pre>
