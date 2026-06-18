---
description: Use KernelPlatform.GetTerminalEmulator()
icon: chart-mixed
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/kernel-modifications/analyzer-diagnostics/kernel-nks0042
---

# Kernel - NKS0042

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>Environment.GetEnvironmentVariable("TERM_PROGRAM")</code> instead of <code>KernelPlatform.GetTerminalEmulator()</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>KernelPlatform.GetTerminalEmulator()</code> instead of <code>Environment.GetEnvironmentVariable("TERM_PROGRAM")</code></td></tr><tr><td>Description</td><td><code>KernelPlatform.GetTerminalEmulator()</code> is more readable and less verbose than <code>Environment.GetEnvironmentVariable("TERM_PROGRAM")</code>.</td></tr></tbody></table>

***

## <mark style="color:$primary;">Extended Description</mark>

This code analyzer detects the usage of `GetEnvironmentVariable("TERM_PROGRAM")` from the `Environment` class found in the `System` namespace.

`GetEnvironmentVariable` is a method to determine the terminal emulator and the terminal type. It's also a method to determine whether it's running on GNU Screen or on Tmux. However, we needed to increase the readability.

As a result, `KernelPlatform` implements a handful of terminal detection functions to simplify the complicated terminal checking statements to its simpler equivalent.

***

## <mark style="color:$primary;">Analysis Comparison</mark>

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

### <mark style="color:$primary;">Before the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    var value = Environment.GetEnvironmentVariable("TERM_PROGRAM");
</strong>}
</code></pre>

### <mark style="color:$primary;">After the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    var value = KernelPlatform.GetTerminalEmulator();
</strong>}
</code></pre>
