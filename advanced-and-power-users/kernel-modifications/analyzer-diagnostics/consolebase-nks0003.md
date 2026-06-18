---
description: Use SetTitle() from ConsoleExtensions
icon: chart-mixed
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/kernel-modifications/analyzer-diagnostics/consolebase-nks0003
---

# ConsoleBase - NKS0003

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>Console.Title</code> instead of <code>SetTitle()</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>SetTitle()</code> instead of <code>Console.Title</code></td></tr><tr><td>Description</td><td><code>SetTitle()</code> uses the VT sequence to set the title, while <code>Console.Title</code> works in certain conditions.</td></tr></tbody></table>

***

## <mark style="color:$primary;">Extended Description</mark>

This code analyzer detects the usage of `Title` from the standard `Console` class found in the `System` namespace. Based on our earlier tests with TMUX and Unix consoles, we've concluded that the VT sequence approach is better than using the normal `Console.Title` setter.

***

## <mark style="color:$primary;">Analysis Comparison</mark>

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

### <mark style="color:$primary;">Before the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction() =>
<strong>    Console.Title = "Hello, world!";
</strong></code></pre>

### <mark style="color:$primary;">After the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction() =>
<strong>    ConsoleMisc.SetTitle("Hello, world!");
</strong></code></pre>
