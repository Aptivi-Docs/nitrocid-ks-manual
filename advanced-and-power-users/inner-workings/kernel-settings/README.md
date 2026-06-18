---
description: How settings works.
icon: wrench
---

# Kernel Settings

The kernel is extensively configurable. It allows you to customize your kernel to fit your needs across all areas, ranging from general kernel settings to networking to screensavers. It's an exciting feature!

## How it works?

The kernel configuration files are stored in the below software paths (`Paths.AppDataPath` under the `KS.Files` namespace):

* Windows: `%localappdata%\KS\`
* Linux: `~/.config/ks/`

When the kernel starts up, different configuration files are read for different purposes. The below settings paths describe the purpose and the type of each (with all the addons).

```
d-----          7/5/2024   4:17 PM                KSContacts
d-----          7/5/2024   4:15 PM                KSContactsImport
d-----          6/1/2024   4:41 PM                KSEvents
d-----          6/1/2024   4:49 PM                KSMods
d-----          6/1/2024   4:41 PM                KSReminders
-a----         6/20/2024   7:50 PM              2 Aliases.json
-a----         12/4/2024  11:58 PM            270 AmusementsConfig.json
-a----         12/4/2024  11:58 PM            718 AmusementsSaversConfig.json
-a----         12/4/2024  11:58 PM             38 AmusementsSplashesConfig.json
-a----         12/4/2024  11:58 PM             40 ArchiveConfig.json
-a----         12/4/2024  11:58 PM             44 BassBoomConfig.json
-a----         12/4/2024  11:58 PM             28 BassBoomSaversConfig.json
-a----         12/4/2024  11:58 PM             49 CalendarConfig.json
-a----         12/4/2024  11:58 PM              2 Consents.json
-a----         12/4/2024  11:58 PM             26 ContactsConfig.json
-a----         12/4/2024  11:58 PM             22 ExtensionHandlers.json
-a----         12/4/2024  11:58 PM          31717 ExtraSaversConfig.json
-a----         12/4/2024  11:58 PM            234 ExtraSplashesConfig.json
-a----         12/4/2024  11:58 PM             26 ForecastConfig.json
-a----         12/4/2024  11:58 PM            554 FtpConfig.json
-a----         12/4/2024  11:58 PM             36 GitConfig.json
-a----         12/4/2024  11:58 PM             42 HttpConfig.json
-a----         12/4/2024  11:58 PM            139 JsonConfig.json
-a----         6/20/2024   7:50 PM            285 KernelCustomSettings.json
-a----         7/11/2024   6:51 PM        2780957 kernelDbg-0.log
-a----         12/4/2024  11:58 PM            484 KernelDriverConfig.json
-a----         12/4/2024  11:58 PM           7632 KernelMainConfig.json
-a----         12/4/2024  11:58 PM             92 KernelSaverConfig.json
-a----         12/4/2024  11:58 PM             35 KernelSplashConfig.json
-a----         12/4/2024  11:58 PM            856 KernelWidgetsConfig.json
-a----          6/1/2024   4:42 PM          42570 KSJournal-0.json
-a----         12/4/2024  11:58 PM            512 MailConfig.json
-a----         6/20/2024   7:50 PM             48 MAL.txt
-a----         6/20/2024   7:50 PM             48 MOTD.txt
-a----         12/4/2024  11:58 PM            218 NameGenSaversConfig.json
-a----         6/11/2024   5:56 PM             24 notes.json
-a----         12/4/2024  11:58 PM            157 RssConfig.json
-a----         12/4/2024  11:58 PM            143 SftpConfig.json
-a----         12/4/2024  11:58 PM           2315 ShellHistories.json
-a----         6/22/2024   5:20 PM            260 SpeedDial.json
-a----         12/4/2024  11:58 PM             41 SqlConfig.json
-a----         12/4/2024  11:58 PM             73 SshConfig.json
-a----         12/4/2024  11:58 PM             70 StocksConfig.json
-a----         12/4/2024  11:58 PM             64 TimersConfig.json
-a----         12/4/2024  11:58 PM             23 TipsConfig.json
-a----          6/1/2024   4:41 PM              4 ToDoList.json
-a----          6/1/2024   4:41 PM              2 UserGroups.json
-a----          9/7/2024   9:51 PM            795 Users.json
```

## Settings

<figure><img src="../../../.gitbook/assets/101-settings.png" alt=""><figcaption></figcaption></figure>

The kernel provides an easy-to-use tool to seamlessly configure the kernel settings. It can be easily invoked using the `settings` command. Running this command alone provides you with the normal kernel settings. The following switches will change the mode:

* `-saver`: Lets you configure the screensavers
* `-addonsaver`: Lets you configure the screensavers from the Extra Screensavers addon
* `-splash`: Lets you configure the splashes
* `-addonsplash`: Lets you configure the splashes from the Extra Splashes addon
* `-driver`: Lets you configure the kernel drivers
* `-widgets`: Lets you configure the kernel widgets for the lockscreen
* `-type=configType`: Lets you configure a custom section of the kernel settings, including your mod-defined ones.

{% hint style="info" %}
Currently, the settings application uses Terminaux's interactive TUI feature. If you still prefer the selection style to the TUI, you can pass the `-sel` switch.
{% endhint %}

Selecting a section leads to the settings application listing all the available configuration options, which you can then set their individual options. It even allows you to save the settings if you like the current configuration, load the user settings, and find a settings entry for easier access.

{% hint style="success" %}
Starting from 0.1.0.5, you can easily migrate most of your kernel configuration, including your speed dial settings, from the old format that 0.0.16.0 introduced back on 2021. Just open the settings app and select "Migrate old configuration."
{% endhint %}

{% hint style="danger" %}
We'll never support configuration migration for older formats, such as the `.ini` format that 0.0.4 introduced, due to deprecation of API versions 1.0, 1.1, and 1.2.
{% endhint %}

### System updates and information

From the main page, you can easily check for kernel updates and check the system information right from it.

### Inner workings

You can find more information about the mechanics of the settings application by clicking on the below link.

{% content-ref url="mechanics-of-settings-app.md" %}
[mechanics-of-settings-app.md](mechanics-of-settings-app.md)
{% endcontent-ref %}

## Settings on your Shell

Additionally, you can change the kernel settings and list them using the following available commands:

* `lsconfigs`: This command allows you to list all configurations and their entries.
* `lsconfigvalues`: This command allows you to list all configuration keys and their values
* `getconfigvalue`: This command allows you to get a config value by the variable name
* `setconfigvalue`: This command allows you to set a config value by the variable name to the specified value

This feature is useful for your UESH scripts and for your quick shortcut to change your settings.

## Settings format

The settings format is out of scope for this page, so click the below link to learn more.

{% content-ref url="settings-format.md" %}
[settings-format.md](settings-format.md)
{% endcontent-ref %}

## Custom settings

The custom settings and its relationship with your mods is out of scope for this page, so click the below link to learn more.

{% content-ref url="custom-settings.md" %}
[custom-settings.md](custom-settings.md)
{% endcontent-ref %}
