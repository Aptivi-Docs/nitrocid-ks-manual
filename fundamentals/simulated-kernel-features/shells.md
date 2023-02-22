---
description: What are the shells?
---

# 🐚 Shells

<figure><img src="../../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

Operating systems contain their shells that listen to user input and execute any command – either built-in or custom – to perform operations that the users plan or need to do. Shells usually contain the prompt indicator to tell the user where is the current working directory, the user name, the host name, or anything that is set up to show.

In Linux systems, the shell is initiated with the help of both the log-in handler and the system initialization program, usually found in `/sbin/init`. Linux shells are numerous, like `zsh`, `dash`, and `bash`. In Windows, it has only two shells, which is PowerShell and Command Prompt (simulates the MS-DOS command prompt).

Each shell contain their own built-in commands and their usage and purpose that are hard-coded to the shell, and they're usually not distributed in a binary form. External commands are just programs or scripts that you would execute, but found in your system drive or any of the drives.

In the simulated kernel, the kernel initialization system only runs one shell, which is Unified Extensible SHell (UESH), that runs more like a shell manager. This shell manager calls for the main shell to be executed the moment the user logs on.

## Unified Extensible SHell (UESH)

This program is part of the core kernel that is programmed to not only be a standalone shell, but also be an extensible shell manager that actually executes built-in and custom shells, supervise the shell's behavior, and manage the shell stack. It provides you an ability to be able to implement your commands for any built-in shells and build your own shell that actually contains your own built-in commands.

For more information about its inner workings and how you can build your own commands and shells, consult the below page.

{% content-ref url="../../advanced-and-power-users/inner-workings/shell-structure/" %}
[shell-structure](../../advanced-and-power-users/inner-workings/shell-structure/)
{% endcontent-ref %}

For scripting, consult the below page.

{% content-ref url="../../advanced-and-power-users/inner-workings/shell-structure/shell-scripting.md" %}
[shell-scripting.md](../../advanced-and-power-users/inner-workings/shell-structure/shell-scripting.md)
{% endcontent-ref %}

## Commands

The main shell contains these commands that you can use below. The administrative commands are listed in the bottom of the list to differentiate from the normal commands.

### Normal commands

* `archive <archivefile>`
  * Opens the archive file to the archive shell
* `beep`
  * Makes a beep from the console
* `bulkrename <targetdir> <pattern> <newname>`
  * Renames the files massively satisfying the pattern to the new name
* `calc <expression>`
  * Calculates the expression
* `calendar <show> [year] [month]`
  * Shows the calendar
* `calendar <event> <add> <date> <title>`
  * Adds an event to the calendar
* `calendar <event> <remove> <eventid>`
  * Removes the event from the calendar
* `calendar <event> <list>`
  * Lists all the events
* `calendar <event> <saveall>`
  * Saves all the events
* `calendar <reminder> <add> <dateandtime> <title>`
  * Adds the reminder to the calendar
* `calendar <reminder> <remove> <reminderid>`
  * Removes the reminder from the calendar
* `calendar <reminder> <list>`
  * Lists all the reminders
* `calendar <reminder> <saveall>`
  * Saves all the reminders
* `cat [-lines|-nolines|-plain] <file>`
  * Prints the contents of a file
* `chattr <file> +/-<attributes>`
  * Changes the attribute of a file
* `chdir <directory/..>`
  * Changes the directory to another directory
* `choice [-o|-t|-m|-a] [-multiple|-single] <$variable> <answers> <input> [answertitle1] [answertitle2] ...`
  * Makes a choice amd sets it to a UESH variable
* `clearfiredevents`
  * Clears the fired events
* `cls`
  * Clears the screen
* `colorhextorgb <#RRGGBB>`
  * Converts the hexadecimal representation of the color to RGB numbers
* `colorhextorgbks <#RRGGBB>`
  * Converts the hexadecimal representation of the color to RGB numbers in KS format
* `colorrgbtohex <R> <G> <B>`
  * Converts the color RGB numbers to a hexadecimal representation
* `combinestr <input1> <input2> [input3] ...`
  * Combines the strings
* `combine <output> <input1> <input2> [input3] ...`
  * Combines the two or more text files to the output
* `convertlineendings <textfile> [-w|-u|-m]`
  * Converts the line endings to the current platform line ending or a specific line ending
* `copy <source> <target>`
  * Creates another copy of a source file under the target
* `dict <word>`
  * Defines a word
* `dirinfo <directory>`
  * Provides information about a directory
* `dismissnotif <notificationNumber>`
  * Dismisses a notification
* `dismissnotifs`
  * Dismisses all notifications
* `echo [text]`
  * Echoes a text
* `edit <file>`
  * Edits a file
* `fileinfo <file>`
  * Provides information about a file
* `find <file> [directory]`
  * Finds a file in the specified directory or a current directory
* `ftp [server]`
  * Use an FTP shell to interact with the FTP server
* `genname [-t] [namescount] [nameprefix] [namesuffix] [surnameprefix] [surnamesuffix]`
  * Name and surname generator
* `gettimeinfo <date>`
  * Gets the date and time information
* `get <URL>`
  * Downloads a file to the current working directory
* `hangman`
  * Starts the Hangman game
* `http`
  * Starts the HTTP shell
* `hwinfo <HardwareType/all>`
  * Lists the hardware info
* `if <uesh-expression> <command>`
  * If the expression is satisfied, executes a command
* `ifm`
  * Interactive file manager
* `input <$variable> <question>`
  * Allows user to enter input and save it to a specified UESH variable
* `jsonbeautify <jsonfile> [output]`
  * Beautifies a JSON file
* `jsonminify <jsonfile> [output]`
  * Minifies a JSON file
* `keyinfo`
  * Gets key information for a pressed key
* `license`
  * Shows license information for the kernel
* `lintscript <script>`
  * Checks your UESH script for syntax errors
* `list [-showdetails|-suppressmessages|-recursive] [directory]`
  * Lists either the current directory or a specified directory
* `listunits <type>`
  * Lists all available units
* `lockscreen`
  * Locks your screen
* `logout`
  * Logs you out
* `lsusers`
  * Lists the users
* `lsvars`
  * Lists the set UESH variables
* `mail [emailAddress]`
  * Opens the mail client
* `md <directory>`
  * Creates a directory
* `meteor`
  * You are a spaceship and the meteors are coming to destroy you. Can you save it?
* `mkfile <file>`
  * Makes a normal file
* `mktheme <themeName>`
  * Opens the theme studio to let you create a new theme
* `modmanual [-list] <ManualTitle>`
  * Opens the manual viewer for your mod manual
* `move <source> <target>`
  * Moves a file or directory to the target
* `open <URL>`
  * Opens a URL
* `ping [times] <Address1> <Address2> ...`
  * Pings an address
* `playlyric <lyric.lrc>`
  * Plays a lyric file
* `previewsplash [splashName]`
  * Previews a splash
* `put <FileName> <URL>`
  * Uploads a file to specified website
* `reboot [ip] [port]`
  * Restarts the simulated kernel
* `retroks`
  * Starts the Retro Kernel Simulator
* `rm <directory/file>`
  * Removes a directory or file
* `reportbug`
  * A bug reporting prompt
* `roulette`
  * Russian Roulette
* `rss [-m] [feedlink]`
  * Opens the RSS feed
* `savescreen [saver]`
  * Saves your screen
* `search <Regexp> <File>`
  * Searches for specified file using the regular expression
* `searchword <StringEnclosedInDoubleQuotes> <File>`
  * Searches for specified file using the string
* `select <$variable> <answers> <input> [answertitle1] [answertitle2] ...`
  * Provides a selection choice
* `set <$variable> <value>`
  * Sets a value to a variable
* `setrange <$variablename> <value1> [value2] [value3] ...`
  * Creates a variable array with set variables
* `sftp`
  * Lets you use an SSH FTP server
* `shownotifs`
  * Shows all the received notifications
* `showtd`
  * Shows time and date
* `showtdzone [-all] <timezone>`
  * Shows time and date in a timezone
* `shutdown [ip] [port]`
  * Shuts down the kernel
* `sleep <ms>`
  * Sleeps for specified milliseconds
* `snaker`
  * The snake game!
* `solver`
  * Starts the Solver game!
* `speedpress [-e|-m|-h|-v|-c] [timeout]`
  * Starts the SpeedPress game!
* `sshell <address:port> <username>`
  * Connects to an SSH server
* `sshcmd <address:port> <username> "<command>"`
  * Connects to an SSH server to execute a command
* `stopwatch`
  * A simple stopwatch
* `sumfile [-relative] <MD5/SHA1/SHA256/SHA384/SHA512/all> <file> [outputFile]`
  * Calculates a file sum
* `sumfiles [-relative] <MD5/SHA1/SHA256/SHA384/SHA512/all> <dir> [outputFile]`
  * Calculates sum of files
* `themesel [Theme]`
  * Selects a theme and sets it
* `timer`
  * A simple timer
* `unitconv <unittype> <quantity> <sourceunit> <targetunit>`
  * Unit converter
* `unzip <zipfile> [path] [-createdir]`
  * Extracts a ZIP archive
* `usermanual [-modapi]`
  * Opens this documentation website
* `verify <MD5/SHA1/SHA256/SHA384/SHA512> <calculatedhash> <hashfile/expectedhash> <file>`
  * Verifies sanity of the file
* `weather [-list] <CityID/CityName> [apikey]`
  * Shows weather info for specified city using OpenWeatherMap
* `wordle [-orig]`
  * Starts the Wordle game
* `wrap <command>`
  * Wraps the console output
* `zip <zipfile> <path> [-fast|-nocomp|-nobasedir]`
  * Creates a ZIP archive

### Administrative commands

* `adduser <userName> [password] [confirm]`
  * Adds a new user to the kernel
* `admin`
  * Opens the administrative shell
* `alias <rem/add> <ShellType> <alias> <cmd>`
  * Manages the aliases, like adding and removing aliases
* `blockdbgdev <ipaddress>`
  * Blocks the connected debug device
* `chhostname <HostName>`
  * Changes the host name
* `chmal [Message]`
  * Changes the MOTD After Login (MAL) either by specifying the message or by opening the text editor to the MAL configuration file
* `chmotd [Message]`
  * Changes the Message of the Day (MOTD) either by specifying the message or by opening the text editor to the MOTD configuration file
* `chpwd <Username> <UserPass> <newPass> <confirm>`
  * Changes the password of a user. If the user contains no password, leave the second argument empty
* `chusrname <oldUserName> <newUserName>`
  * Changes the user name
* `disconndbgdev <ip>`
  * Disconnects the debug device
* `langman <reload/load/unload> <customlanguagename>`
  * Loads and unloads the custom language
* `langman <list/reloadall>`
  * Lists or reloads all the custom languages
* `lsdbgdev`
  * Lists all the connected debug devices
* `lsnet`
  * Lists all the online network devices
* `modman <start/stop/info/reload/install/uninstall> <modfilename>`
  * Manages a specific mod
* `modman <list/listparts> [modname]`
  * Lists all the available mods or parts of a mod
* `modman <reloadall/stopall/startall>`
  * Manages all the mods at once
* `perm <userName> <allow/revoke> <perm>`
  * Manages the user permissions
* `reloadconfig`
  * Reloads the configuration file (invoke if the config file is edited externally)
* `reloadsaver <customsaver>`
  * Reloads a custom screensaver file
* `rexec <address> [port] <command>`
  * Remotely executes an RPC command to another computer running Nitrocid KS with RPC enabled
* `rdebug`
  * Enables or disables the remote debugging
* `rmuser <Username>`
  * Removes a user
* `savecurrdir`
  * Saves the current directory to the kernel configuration file
* `setsaver <customsaver/builtinsaver>`
  * Sets the default screensaver to a built-in screensaver or a custom screensaver
  * _This command is obsolete and should be avoided. This setting can be set using the `settings` command under `Screensaver Settings.`_
* `settings [-saver|-splash]`
  * Opens the settings application in either the normal mode, screensaver mode, or splash mode
* `taskman`
  * Task management
* `unblockdbgdev <ipaddress>`
  * Unblocks a debug device
* `update`
  * Checks for updates of the kernel and downloads the update if available
