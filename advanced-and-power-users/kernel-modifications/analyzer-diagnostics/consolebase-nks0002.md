---
description: Use ConsoleWrapper instead of Console
icon: chart-mixed
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/kernel-modifications/analyzer-diagnostics/consolebase-nks0002
---

# ConsoleBase - NKS0002

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>Console</code> instead of <code>ConsoleWrapper</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>ConsoleWrapper</code> instead of <code>Console</code></td></tr><tr><td>Description</td><td><code>ConsoleWrapper</code> makes sure that your console is not a dumb console. This class is a wrapper for the <code>Console</code> class so that it works cross-platform, while <code>Console</code> contains some platform-dependent APIs.</td></tr></tbody></table>

***

## <mark style="color:$primary;">Extended Description</mark>

This code analyzer detects the usage of the standard `Console` class found in the `System` namespace. However, this class is a sealed class, so it's rendered inextensible, causing you to have to make its abstraction class to wrap its functions if you want to add extra code, like checking for VT sequences.

Fortunately, Terminaux has a console wrapper, `ConsoleWrapper`, that makes use of the current local console driver that contains the necessary checks, like checking the console for its fullness (positioning and any other functions other than plain writing). It's connected to the local console driver that Nitrocid KS manages.

So, if you want to use the `Console` class, you must replace these calls with `ConsoleWrapper` to take advantage of the local console drivers.

Furthermore, some of the wrapper functions are used by the much powerful console writers, like `TextWriterColor.Write()`, that include sanity checks before actually doing the job.

***

## <mark style="color:$primary;">Analysis Comparison</mark>

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

### <mark style="color:$primary;">Before the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction() =>
<strong>    Console.WriteLine("Hello, world!");
</strong></code></pre>

### <mark style="color:$primary;">After the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction() =>
<strong>    ConsoleWrapper.WriteLine("Hello, world!");
</strong></code></pre>
