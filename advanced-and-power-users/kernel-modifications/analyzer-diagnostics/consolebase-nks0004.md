---
description: Use SetConsoleColor(Color) from KernelColorTools
icon: chart-mixed
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/kernel-modifications/analyzer-diagnostics/consolebase-nks0004
---

# ConsoleBase - NKS0004

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>Console.ForegroundColor</code> instead of <code>SetConsoleColor(Color)</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>SetConsoleColor(Color)</code> instead of <code>Console.ForegroundColor</code></td></tr><tr><td>Description</td><td><code>SetConsoleColor(Color)</code> not only brings better color support provided by the appropriate VT sequences, but it can also use true color. <code>Console.ForegroundColor</code> only handles 16 colors.</td></tr></tbody></table>

***

## <mark style="color:$primary;">Extended Description</mark>

This code analyzer detects the usage of `ForegroundColor` from the standard `Console` class found in the `System` namespace. This property only supports up to 16 colors, and, in order to upgrade to 255 colors or true color, you need to have a console that supports it and a VT escape sequence to be able to set the foreground color of the console in any color you want.

As a result, `SetConsoleColor` simplifies things up by using the `Color` class provided by Terminaux to be able to set the color without being restricted to the domain of the 16 colors.

***

## <mark style="color:$primary;">Analysis Comparison</mark>

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

### <mark style="color:$primary;">Before the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction() =>
<strong>    Console.ForegroundColor = ConsoleColor.Green;
</strong></code></pre>

### <mark style="color:$primary;">After the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction() =>
<strong>    ConsoleColoring.SetConsoleColor(ConsoleColors.Green);
</strong></code></pre>
