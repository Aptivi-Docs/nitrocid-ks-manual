---
description: Use NetworkTools.NetworkAvailable
icon: chart-mixed
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/kernel-modifications/analyzer-diagnostics/network-nks0051
---

# Network - NKS0051

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>NetworkInterface.GetIsNetworkAvailable</code> instead of <code>NetworkTools.NetworkAvailable</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>NetworkTools.NetworkAvailable</code> instead of <code>NetworkInterface.GetIsNetworkAvailable</code></td></tr><tr><td>Description</td><td>While <code>NetworkInterface.GetIsNetworkAvailable</code> checks your network, it doesn't work on Android systems, so it's better to use <code>NetworkTools.NetworkAvailable</code>. Please note that this will return <code>false</code> if there is no connectivity for Android systems.</td></tr></tbody></table>

***

## <mark style="color:$primary;">Extended Description</mark>

This code analyzer detects the usage of `GetIsNetworkAvailable` from the `NetworkInterface` class found in the `System.Net.NetworkInformation` namespace.

Normally, `NetworkInterface.GetIsNetworkAvailable` would return true if there are network interfaces that are ready to connect (their state is UP). However, this approach doesn't work on Android systems as Nitrocid doesn't build for Xamarin.Android, which has the necessary libraries for Java bindings to the Android API.

As a result, you'll have to use the sensible `NetworkTools.NetworkAvailable` property to allow you to check to see if there are ready network interfaces. Please note that if you have no working internet connection, even if your WiFi is turned on in your Android device, it'll report as false.

***

## <mark style="color:$primary;">Analysis Comparison</mark>

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

### <mark style="color:$primary;">Before the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    bool available = NetworkInterface.GetIsNetworkAvailable;
</strong>}
</code></pre>

### <mark style="color:$primary;">After the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    bool available = NetworkTools.NetworkAvailable;
</strong>}
</code></pre>
