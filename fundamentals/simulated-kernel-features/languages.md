---
description: Multilingual Kernel!
---

# 🇺🇸 Languages

<figure><img src="../../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

Localization was implemented when computers were distributed in non-English countries to aid the users in using their computers in their native language. This feature is currently supported in both Windows and Unix-based operating systems.

However, Linux boot messages don't get localized unless the localization is set, which is done in the middle of the boot process. This simulator attempts to localize the boot messages in the start of the process.

You can set the language using the `settings` command under the `General` section. Any language changes will be saved to the configuration file.

Languages usually get translated at the end of each development period of each upcoming kernel version. It's normal to see untranslated string indicators, which the text is usually surrounded with the `(( ))` signs. If you still see these signs in the final version, report it to us [using this page](https://github.com/Aptivi/Kernel-Simulator/issues/new).

### Changing the language

<figure><img src="../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

To change the simulated kernel language, follow these steps:

1. Log-in to the system account, root, or any of the administrators or users that has at least the settings management permission
2. Execute the `settings` command, go to `General`, and go to `Language`
3. Select a new language

{% hint style="info" %}
Note that your account must have either the administrative permissions enabled or the settings management permission granted to be able to use this command.
{% endhint %}
