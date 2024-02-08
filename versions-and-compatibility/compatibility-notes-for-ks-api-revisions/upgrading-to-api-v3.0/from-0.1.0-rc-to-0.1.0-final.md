---
description: Guide for upgrading 0.1.0 RC mods to 0.1.0 Final
---

# ⬆ From 0.1.0 RC to 0.1.0 Final

This page lists all the changes that have been made from 0.1.0 RC to 0.1.0 Final. For upgrading your mods from 0.0.24.x directly to the 0.1.0 series, use the main upgrade page instead.

### Enumerable tools moved to EnumMagic

{% code title="EnumerableTools.cs" lineNumbers="true" %}
```csharp
public static class EnumerableTools
```
{% endcode %}

We've moved `EnumerableTools`, which holds non-generic enumerable interface tools that make jobs easier, from Nitrocid to EnumMagic as we needed to make it more open to the public. This is to ensure that these extensions get used by different libraries, such as Terminaux.

{% hint style="info" %}
You'll need to reference EnumMagic in order to use the tools.
{% endhint %}

### Moved three hashing algorithms

<pre class="language-csharp" data-title="DriverHandler.cs" data-line-numbers><code class="lang-csharp">internal static Dictionary&#x3C;DriverTypes, Dictionary&#x3C;string, IDriver>> drivers = new()
{
    (...)
    {
        DriverTypes.Encryption, new()
        {
            { "Default", new SHA256() },
<strong>            { "MD5", new MD5() },
</strong><strong>            { "SHA1", new SHA1() },
</strong>            { "SHA256", new SHA256() },
<strong>            { "SHA384", new SHA384() },
</strong>            { "SHA512", new SHA512() }
        }
    },
    (...)
}
</code></pre>

The three hashing algorithms have been moved to their own individual addons:

* `Nitrocid.Extras.Md5`
* `Nitrocid.Extras.Sha1`
* `Nitrocid.Extras.Sha384`

As a result, your mods will break if they assume that these three algorithms are installed as built-in, which is the case for RC and earlier beta versions of 0.1.0. The reason of that is because of security.

{% hint style="info" %}
Your mods will break only if they have been used and the three addons are not installed yet.
{% endhint %}
