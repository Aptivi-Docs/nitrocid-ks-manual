---
description: How settings works.
---

# 🔧 Kernel Settings

The kernel is extensively configurable. It allows you to customize your kernel to fit your needs across all areas, ranging from general kernel settings to networking to screensavers. It's an exciting feature!

## How it works?

The kernel configuration files are stored in the below software paths (`Paths.AppDataPath` under the `KS.Files` namespace):

* Windows: `%localappdata%\KS\`
* Linux: `~/.config/ks/`

When the kernel starts up, different configuration files are read for different purposes. The below settings paths describe the purpose and the type of each.

* Configuration: `KernelConfig.json`
  * Description: Stores all the main kernel configuration
  * Type: JSON
  * Location: `Paths.ConfigurationPath` under the `KS.Files` namespace
* Aliases: `Aliases.json`
  * Description: Stores all the user-defined aliases
  * Type: JSON
  * Location: `Paths.AliasesPath` under the `KS.Files` namespace
* Users: `Users.json`
  * Description: Stores all the users
  * Type: JSON
  * Location: `Paths.UsersPath` under the `KS.Files` namespace
* FTP Speed Dial: `FTP_SpeedDial.json`
  * Description: Stores all the saved FTP connections
  * Type: JSON
  * Location: `Paths.FTPSpeedDialPath` under the `KS.Files` namespace
* SFTP Speed Dial: `SFTP_SpeedDial.json`
  * Description: Stores all the saved SFTP connections
  * Type: JSON
  * Location: `Paths.SFTPSpeedDialPath` under the `KS.Files` namespace
* Remote Debug Device Names: `DebugDevicesNames.json`
  * Description: Stores all the remote debug device names
  * Type: JSON
  * Location: `Paths.DebugDevNamesPath` under the `KS.Files` namespace
* MOTD: `MOTD.txt`
  * Description: Stores the message of the day
  * Type: Text file
  * Location: `Paths.MOTDPath` under the `KS.Files` namespace
* MAL: `MAL.txt`
  * Description: Stores the message of the day after login
  * Type: Text file
  * Location: `Paths.MALPath` under the `KS.Files` namespace
* Custom Screensaver Settings: `CustomSaverSettings.json`
  * Description: Stores the message of the day
  * Type: JSON
  * Location: `Paths.CustomSaverSettingsPath` under the `KS.Files` namespace

You can consult the files used by KS for available kernel settings [here](https://github.com/Aptivi/Kernel-Simulator/blob/master/public/Kernel%20Simulator/Resources/Settings/SettingsEntries.json), the screensaver settings [here](https://github.com/Aptivi/Kernel-Simulator/blob/master/public/Kernel%20Simulator/Resources/Settings/ScreensaverSettingsEntries.json), and the splash settings [here](https://github.com/Aptivi/Kernel-Simulator/blob/master/public/Kernel%20Simulator/Resources/Settings/SplashSettingsEntries.json). These files also contain descriptions for each settings entry.

## Settings

<figure><img src="../../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

The kernel provides an easy-to-use tool to seamlessly configure the kernel settings. It can be easily invoked using the `settings` command. Running this command alone provides you with the normal kernel settings. The two switches will change the mode:

* `-saver`: Lets you configure the screensavers
* `-splash`: Lets you configure the splashes

Selecting a section leads to the settings application listing all the available configuration options, which you can then set their individual options. It even allows you to save the settings if you like the current configuration, load the user settings, and find a settings entry for easier access.

### Inner workings

You can find more information about the mechanics of the settings application by clicking on the below link.

{% content-ref url="mechanics-of-settings-app.md" %}
[mechanics-of-settings-app.md](mechanics-of-settings-app.md)
{% endcontent-ref %}

## Settings format

The settings format is out of scope for this page, so click the below link to learn more.

{% content-ref url="settings-format.md" %}
[settings-format.md](settings-format.md)
{% endcontent-ref %}
