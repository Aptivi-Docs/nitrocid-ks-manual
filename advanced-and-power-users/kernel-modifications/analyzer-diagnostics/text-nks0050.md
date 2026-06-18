---
description: Use TextTools.SplitNewLines()
icon: chart-mixed
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/kernel-modifications/analyzer-diagnostics/text-nks0050
---

# Text - NKS0050

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>CharManager.NewLine</code> instead of <code>TextTools.SplitNewLines()</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>TextTools.SplitNewLines()</code> instead of <code>CharManager.NewLine</code></td></tr><tr><td>Description</td><td><code>TextTools.SplitNewLines()</code> simplifies the readability of the split by new lines function.</td></tr></tbody></table>

***

## <mark style="color:$primary;">Extended Description</mark>

This code analyzer detects the usage of `Split(CharManager.NewLine)` from the `String` class found in the `System` namespace.

Splitting by new lines is a good way to get the lines from your string. However, the complexity needs to be reduced so that more readability is achieved. As a result, `SplitNewLines()` is here to do it in the simplest way possible.

***

## <mark style="color:$primary;">Analysis Comparison</mark>

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

### <mark style="color:$primary;">Before the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
    string var = "Hello\nWorld!";
<strong>    var split = var.Split(CharManager.NewLine);
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
