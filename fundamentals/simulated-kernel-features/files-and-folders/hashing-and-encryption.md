---
description: We need to verify your files.
icon: key-skeleton
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/fundamentals/simulated-kernel-features/files-and-folders/hashing-and-encryption
---

# Hashing and Encryption

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

When it comes to verifying the file integrity, the file hashing feature of Nitrocid KS's simulated filesystem comes into play. It features built-in file hashing techniques to allow you to check the sanity of your files. The kernel file encryption features are handled by your selected encryption kernel driver, which can be found here:

{% content-ref url="../../../advanced-and-power-users/inner-workings/inner-essentials/kernel-drivers/encryption-drivers.md" %}
[encryption-drivers.md](../../../advanced-and-power-users/inner-workings/inner-essentials/kernel-drivers/encryption-drivers.md)
{% endcontent-ref %}

Expand a section to get started.

<details>

<summary>Calculating a hash sum</summary>

This part of the entire encryption feature for files is a crucial part, because it involves using your encryption driver to let you get a hash sum for a file or a text. This is also used to calculate the hash sum for a file prior to verification to check to see if your file is tampered with or not.

#### <mark style="color:$primary;">Usage</mark>

The following commands are available for you to try out:

<table><thead><tr><th width="119.66668701171875">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>sumfile</code></td><td>Allows you to get a hash sum for a single file</td></tr><tr><td><code>sumfiles</code></td><td>Allows you to get a hash sum for a single directory</td></tr><tr><td><code>sumtext</code></td><td>Allows you to get a hash sum for a text</td></tr></tbody></table>

#### <mark style="color:$primary;">Tools</mark>

In the `Encryption` class found in the `Nitrocid.Drivers.Encryption` namespace, you can access the hashing tools to give your mods ability to use the current encryption driver to encrypt your files and your texts.

The following functions are available:

* `GetEncryptedString()`
* `GetEncryptedFile()`

</details>

<details>

<summary>Verifying a hash sum</summary>

<figure><img src="../../../.gitbook/assets/image (2) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

You can also use the verification feature in both the main command-line shell and in your mod's code to allow you to check a file to see if the two hashes (calculated or not) match or not. This works under the following two conditions:

* If the verification part concludes that the two hashes match, your file is fine.
* If the verification part concludes that the two hashes don't match, your file is tampered with.

#### <mark style="color:$primary;">Usage</mark>

The following commands are available for you to try out:

<table><thead><tr><th width="119.66668701171875">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>verify</code></td><td>Allows you to verify your file or your hash</td></tr></tbody></table>

#### <mark style="color:$primary;">Tools</mark>

In the `HashVerifier` class found in the `Nitrocid.Drivers.Encryption` namespace, you can access the verifier tools to give your mods ability to use the current encryption driver to verify the hash sum of your files and your texts.

The following functions are available:

* `VerifyHashFromHashesFile()`
* `VerifyHashFromHash()`
* `VerifyUncalculatedHashFromHashesFile()`
* `VerifyUncalculatedHashFromHash()`
* `VerifyHashPlain()`

</details>

<details>

<summary>Performing other operations</summary>

<figure><img src="../../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>

In both the above classes, you can also access the miscellaneous hash and verification tools. The following tools can be used in your mods:

<table><thead><tr><th width="240.33331298828125">Function</th><th>Description</th></tr></thead><tbody><tr><td><code>GetExpectedHashLength()</code></td><td>Gets the expected hash length according to the algorithm</td></tr><tr><td><code>GetArrayEnc()</code></td><td>Gets a string representation of a byte array</td></tr><tr><td><code>GetEmptyHash()</code></td><td>Gets a hash sum for an empty string</td></tr></tbody></table>

</details>
