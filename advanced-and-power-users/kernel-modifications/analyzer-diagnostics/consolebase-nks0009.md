---
description: Use ConsoleTools.ResetColors()
icon: chart-mixed
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/kernel-modifications/analyzer-diagnostics/consolebase-nks0009
---

# ConsoleBase - NKS0009

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>Console.ResetColor</code> instead of <code>ThemeColorsTools.ResetColors()</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>ThemeColorsTools.ResetColors()</code> instead of <code>Console.ResetColor</code></td></tr><tr><td>Description</td><td><code>ThemeColorsTools.ResetColors()</code> contains VT sequences that help reset colors in a portable way.</td></tr></tbody></table>

***

## <mark style="color:$primary;">Extended Description</mark>

This code analyzer detects the usage of `ResetColor` from the standard `Console` class found in the `System` namespace.

While `ResetColor()` is enough to reset all the colors, we felt that using simple VT sequences to achieve the same goal is more viable. Therefore, we've made the `ResetColors()` function that allows you to simply reset the colors.

***

## <mark style="color:$primary;">Analysis Comparison</mark>

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

### <mark style="color:$primary;">Before the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    Console.ResetColor();
</strong>}
</code></pre>

### <mark style="color:$primary;">After the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    ThemeColorsTools.ResetColors();
</strong>}
</code></pre>
