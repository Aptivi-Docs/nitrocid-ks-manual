---
description: How settings works.
icon: wrench
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/inner-workings/kernel-settings
---

# Kernel Settings

The kernel is extensively configurable. It allows you to customize your kernel to fit your needs across all areas, ranging from general kernel settings to networking to screensavers. It's an exciting feature!

***

## <mark style="color:$primary;">How it works?</mark>

The kernel configuration files are stored in the below software paths (`Paths.AppDataPath` under the `KS.Files` namespace):

* Windows: `%localappdata%\KS\`
* Linux: `~/.config/ks/`

When the kernel starts up, different configuration files are read for different purposes.

<details>

<summary>Nitrocid configuration file structure</summary>

The below settings paths describe the purpose and the type of each (with all the addons).

{% code expandable="true" %}
```
Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----        12/16/2025   1:00 PM                HomepagePages
d-----        12/16/2025  12:59 PM                KSEvents
d-----        12/16/2025  12:59 PM                KSReminders
d-----        12/16/2025   1:00 PM                LogonPages
-a----        12/16/2025   1:00 PM            270 AmusementsConfig.json
-a----        12/16/2025   1:00 PM            933 AmusementsSaversConfig.json
-a----        12/16/2025   1:00 PM             38 AmusementsSplashesConfig.json
-a----        12/16/2025   1:00 PM             45 BassBoomConfig.json
-a----        12/16/2025   1:00 PM             28 BassBoomSaversConfig.json
-a----        12/16/2025   1:00 PM            489 CalendarConfig.json
-a----        12/16/2025   1:00 PM             27 ChatbotAIConfig.json
-a----        12/16/2025   1:00 PM              2 Consents.json
-a----        12/16/2025   1:00 PM             27 ContactsConfig.json
-a----        12/16/2025   1:00 PM            131 DatesConfig.json
-a----        12/16/2025   1:00 PM             22 ExtensionHandlers.json
-a----        12/16/2025   1:00 PM          38056 ExtraSaversConfig.json
-a----        12/16/2025   1:00 PM            273 ExtraSplashesConfig.json
-a----        12/16/2025   1:00 PM             26 ForecastConfig.json
-a----        12/16/2025   1:00 PM            410 KernelDriverConfig.json
-a----        12/16/2025   1:00 PM           7527 KernelMainConfig.json
-a----        12/16/2025   1:00 PM            144 KernelSaverConfig.json
-a----        12/16/2025   1:00 PM             36 KernelSplashConfig.json
-a----        12/16/2025   1:00 PM            856 KernelWidgetsConfig.json
-a----        12/16/2025   1:00 PM              4 KSContacts.json
-a----        12/16/2025   1:00 PM          34766 KSJournal-0.json
-a----        12/16/2025  12:59 PM             23 MAL.txt
-a----        12/16/2025   1:00 PM            129 ModsConfig.json
-a----        12/16/2025  12:59 PM             27 MOTD.txt
-a----        12/16/2025  12:59 PM              2 notes.json
-a----        12/16/2025   1:00 PM           1640 ShellsConfig.json
-a----        12/16/2025   1:00 PM             73 SshConfig.json
-a----        12/16/2025   1:00 PM             54 StocksConfig.json
-a----        12/16/2025   1:00 PM             23 TipsConfig.json
-a----        12/16/2025  12:59 PM              4 ToDoList.json
-a----        12/16/2025  12:59 PM              2 UserGroups.json
-a----        12/16/2025   1:00 PM            714 Users.json
```
{% endcode %}

</details>

***

## <mark style="color:$primary;">Settings</mark>

<figure><img src="../../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

The kernel provides an easy-to-use tool to seamlessly configure the kernel settings. It can be easily invoked using the `settings` command. Running this command alone provides you with the normal kernel settings.

{% hint style="success" %}
Starting from 0.1.0.5, you can easily migrate most of your kernel configuration, including your speed dial settings, from the old format that 0.0.16.0 introduced back on 2021. Just open the settings app and select "Migrate old configuration."
{% endhint %}

<details>

<summary>Available modes via command switches</summary>

The following switches will change the mode:

| Switch             |                                                                                              |
| ------------------ | -------------------------------------------------------------------------------------------- |
| `-saver`           | Lets you configure the screensavers.                                                         |
| `-addonsaver`      | Lets you configure the screensavers from the Extra Screensavers addon.                       |
| `-splash`          | Lets you configure the splashes.                                                             |
| `-addonsplash`     | Lets you configure the splashes from the Extra Splashes addon.                               |
| `-driver`          | Lets you configure the kernel drivers.                                                       |
| `-widgets`         | Lets you configure the kernel widgets for the lock screen.                                   |
| `-type=configType` | Lets you configure a custom section of the kernel settings, including your mod-defined ones. |

</details>

<details>

<summary>Section selection</summary>

Selecting a section leads to the settings application listing all the available configuration options, which you can then set their individual options. It even allows you to save the settings if you like the current configuration, load the user settings, and find a settings entry for easier access.

{% hint style="info" %}
You can change the kernel settings section by either pressing `F9` in the modern settings interface or by highlighting the `Select configuration` option in the classic settings interface.
{% endhint %}

</details>

<details>

<summary>Settings on your shell</summary>

<figure><img src="../../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

This feature is useful for your UESH scripts and for your quick shortcut to change your settings.

You can change the kernel settings and list them using the following available commands:

<table><thead><tr><th width="160">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>lsconfigs</code></td><td>This command allows you to list all configurations and their entries.</td></tr><tr><td><code>lsconfigvalues</code></td><td>This command allows you to list all configuration keys and their values.</td></tr><tr><td><code>getconfigvalue</code></td><td>This command allows you to get a config value by the variable name.</td></tr><tr><td><code>setconfigvalue</code></td><td>This command allows you to set a config value by the variable name to the specified value.</td></tr></tbody></table>

</details>
