---
description: Sometimes we need to check your platform.
icon: computer
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/inner-workings/inner-essentials/kernel-platform
---

# Kernel Platform

<figure><img src="../../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

Sometimes, your mod may contain code that only works on certain platforms. For example, your mod may intentionally call an external unmanaged library's function to do something not normally done in the .NET world using P/Invokes. However, native libraries need to be compiled for the target machines.

Or, you may want to change the behavior of your mod by platform or by how the kernel is started, such as if the kernel was started by the GRILO bootloader.

{% hint style="info" %}
You can check your kernel version and your host RID by going to `settings` and pressing <kbd>F7</kbd> for `System information`.

<img src="../../../.gitbook/assets/image (37).png" alt="" data-size="original">
{% endhint %}

***

## <mark style="color:$primary;">Detection functions</mark>

`KernelPlatform` provides functions to detect platforms and environments. This is to make such tasks relatively easy.

<details>

<summary>Operating systems</summary>

This class provides the following OS-related functions:

<table><thead><tr><th width="150.333251953125">Function</th><th>Description</th></tr></thead><tbody><tr><td><code>IsOnWindows()</code></td><td>Checks to see if Nitrocid KS is running on Windows.</td></tr><tr><td><code>IsOnUnix()</code></td><td>Checks to see if Nitrocid KS is running on Unix and its derivatives, such as Linux, macOS, etc.</td></tr><tr><td><code>IsOnMacOS()</code></td><td>Checks to see if Nitrocid KS is running on Darwin Kernel, the kernel behind macOS.</td></tr><tr><td><code>IsOnAndroid()</code></td><td>Checks to see if Nitrocid KS is running on Android phones and tablets within Termux.</td></tr><tr><td><code>IsOnUnixMusl()</code></td><td>Checks to see if the kernel is running on musl libc library or glibc.</td></tr></tbody></table>

</details>

<details>

<summary>Terminals</summary>

This class provides the following terminal-related functions:

<table><thead><tr><th width="208.9998779296875">Function</th><th>Description</th></tr></thead><tbody><tr><td><code>GetTerminalEmulator()</code></td><td>Gets the terminal emulator name. This may not be accurate.</td></tr><tr><td><code>GetTerminalType()</code></td><td>Gets the terminal emulator name. This may not be accurate.</td></tr></tbody></table>

{% hint style="warning" %}
There are some terminal emulators advertising themselves as XTerm compliant, but actually aren't fully compliant. We advice that you introduce extra checks to ensure that your terminal emulator fully supports the features that you want to use, especially when it comes with the VT sequences.
{% endhint %}

</details>

<details>

<summary>Environments</summary>

This class provides the following environment-related functions:

<table><thead><tr><th width="208.9998779296875">Function</th><th>Description</th></tr></thead><tbody><tr><td><code>IsRunningFromGrilo()</code></td><td>Checks to see whether Nitrocid KS is run from GRILO.</td></tr><tr><td><code>IsRunningFromTmux()</code></td><td>Checks to see whether Nitrocid KS is run on TMUX.</td></tr><tr><td><code>IsRunningFromScreen()</code></td><td>Checks to see whether Nitrocid KS is run on GNU Screen.</td></tr></tbody></table>

</details>

<details>

<summary>CoreCLR</summary>

This class provides the following CoreCLR-related functions:

<table><thead><tr><th width="214.9998779296875">Function</th><th>Description</th></tr></thead><tbody><tr><td><code>GetCurrentRid()</code></td><td>Gets the current runtime identifier.</td></tr><tr><td><code>GetCurrentGenericRid()</code></td><td>Gets the current non-distro-specific runtime identifier.</td></tr></tbody></table>

{% hint style="info" %}
If you're running on a MUSL-based Linux system, `GetCurrentGenericRid()` returns a MUSL-based generic runtime identifier, such as `linux-musl-arm64`.
{% endhint %}

</details>
