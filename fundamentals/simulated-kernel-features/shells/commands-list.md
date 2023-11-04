---
description: List of available commands
---

# 📄 Commands List

This page is a reference that serves as a list of available commands, including the addon commands.

## Built-in commands

Nitrocid KS currently provides the following commands (you can see their definitions in the help command list):

| Commands                | Arguments and Switches                                                           |
| ----------------------- | -------------------------------------------------------------------------------- |
| `addgroup`              | `<groupname>`                                                                    |
| `adduser`               | `<username> [password]`                                                          |
| `addusertogroup`        | `<username> <group>`                                                             |
| `admin`                 |                                                                                  |
| `alias`                 | `<rem/add> <shelltype> <alias> [cmd]`                                            |
| `beep`                  |                                                                                  |
| `blockdbgdev`           | `<ipaddress>`                                                                    |
| `bulkrename`            | `<targetdir> <pattern> [newname]`                                                |
| `cat`                   | `[-lines\|-nolines\|-plain] <file>`                                              |
| `cdir`                  |                                                                                  |
| `chattr`                | `<file> <add/rem> <attr>`                                                        |
| `chdir`                 | `<directory/..>`                                                                 |
| `chhostname`            | `<hostname>`                                                                     |
| `chklock`               | `[-waitforunlock] <file>`                                                        |
| `chlang`                | `[-usesyslang\|-user] <language>`                                                |
| `chmal`                 | `[message]`                                                                      |
| `chmotd`                | `[message]`                                                                      |
| `choice`                | `[-o\|-t\|-m\|-a] [-single\|-multiple] <answers> <input> [title] [title2] [...]` |
| `chpwd`                 | `<username> <pass> <newpass> <newpass>`                                          |
| `chusrname`             | `<oldusername> <newusername>`                                                    |
| `cls`                   |                                                                                  |
| `combinestr`            | `<input> <input2> [input3] [...]`                                                |
| `combine`               | `<output> <input> <input2> [input3] [...]`                                       |
| `convertlineendings`    | `[-w\|-u\|-m] [-force] <text>`                                                   |
| `copy`                  | `<source> <target>`                                                              |
| `date`                  | `[-date\|-time\|-full] [-utc]`                                                   |
| `debugshell`            |                                                                                  |
| `decodefile`            | `[-key] [-iv] <file> [algorithm]`                                                |
| `decodetext`            | `[-key] [-iv] <text> [algorithm]`                                                |
| `dirinfo`               | `<directory>`                                                                    |
| `disconndbgdev`         | `<ip>`                                                                           |
| `diskinfo`              | `<disknum>`                                                                      |
| `dismissnotif`          | `<num>`                                                                          |
| `dismissnotifs`         |                                                                                  |
| `echo`                  | `[-noparse] <text>`                                                              |
| `edit`                  | `[-text\|-sql\|-json\|-hex] <file>`                                              |
| `encodefile`            | `[-key] [-iv] <file> [algorithm]`                                                |
| `encodetext`            | `[-key] [-iv] <text> [algorithm]`                                                |
| `fileinfo`              | `<file>`                                                                         |
| `find`                  | `[-recursive] [-exec] <file> <directory>`                                        |
| `findreg`               | `[-recursive] [-exec] <fileRegex> <directory>`                                   |
| `fork`                  |                                                                                  |
| `ftp`                   | `[server]`                                                                       |
| `get`                   | `[-outputpath] <url>`                                                            |
| `getallexthandlers`     |                                                                                  |
| `getconfigvalue`        | `[-set=variable] <config> <variable>`                                            |
| `getdefaultexthandler`  | `<extension>`                                                                    |
| `getdefaultexthandlers` |                                                                                  |
| `getexthandlers`        | `<extension>`                                                                    |
| `getkeyiv`              | `[algorithm]`                                                                    |
| `host`                  |                                                                                  |
| `http`                  |                                                                                  |
| `hwinfo`                | `<type>`                                                                         |
| `if`                    | `<expression> <command>`                                                         |
| `ifm`                   |                                                                                  |
| `input`                 | `<question>`                                                                     |
| `jsonbeautify`          | `<jsonfile> <output>`                                                            |
| `jsonminify`            | `<jsonfile> <output>`                                                            |
| `langman`               | `<reload/load/unload> <customlangname>`                                          |
|                         | `<list/reloadall>`                                                               |
| `license`               |                                                                                  |
| `lintscript`            | `<script>`                                                                       |
| `list`                  | `[-showdetails\|-suppressmessages\|-recursive] [directory]`                      |
| `lockscreen`            |                                                                                  |
| `logout`                |                                                                                  |
| `lsconfigs`             | `-deep`                                                                          |
| `lsconfigvalues`        | `<config>`                                                                       |
| `lsconnections`         |                                                                                  |
| `lsdbgdev`              |                                                                                  |
| `lsdiskparts`           | `<disknum>`                                                                      |
| `lsdisks`               |                                                                                  |
| `lsexthandlers`         |                                                                                  |
| `lsnet`                 |                                                                                  |
| `lsvars`                |                                                                                  |
| `mail`                  | `[address]`                                                                      |
| `md`                    | `<directory>`                                                                    |
| `mkfile`                | `<file>`                                                                         |
| `modman`                | `<start/stop/info/reload/install/uninstall> <modfilename>`                       |
|                         | `<list/listparts> <modname>`                                                     |
|                         | `<reloadall/stopall/startall>`                                                   |
| `modmanual`             | `<modname>`                                                                      |
| `move`                  | `<source> <target>`                                                              |
| `partinfo`              | `<disknum> <partnum>`                                                            |
| `pathfind`              | `<filename>`                                                                     |
| `perm`                  | `<username> <allow/revoke> <perm>`                                               |
| `permgroup`             | `<groupname> <allow/revoke> <perm>`                                              |
| `ping`                  | `[-times] <address1> [address2] [...]`                                           |
| `platform`              | `[-r\|-v\|-b\|-c\|-n]`                                                           |
| `previewsplash`         | `[-splashout] [-context] <splashname>`                                           |
| `put`                   | `<filename> <url>`                                                               |
| `rdebug`                |                                                                                  |
| `reboot`                | `[ip] [port]`                                                                    |
| `reloadconfig`          |                                                                                  |
| `retroks`               |                                                                                  |
| `rexec`                 | `<address> <port> <command>`                                                     |
| `rm`                    | `<target>`                                                                       |
| `rmsec`                 | `<target>`                                                                       |
| `rmuser`                | `<username>`                                                                     |
| `rmgroup`               | `<groupname>`                                                                    |
| `rmuserfromgroup`       | `<username> <groupname>`                                                         |
| `rss`                   | `[feedlink]`                                                                     |
| `saveconfig`            |                                                                                  |
| `savescreen`            | `[saver]`                                                                        |
| `search`                | `<regex> <file>`                                                                 |
| `searchword`            | `<phrase> <file>`                                                                |
| `select`                | `<answers> <input> [title] [title2] [...]`                                       |
| `setexthandler`         | `<extension> <implementer>`                                                      |
| `setsaver`              | `<saver>`                                                                        |
| `settings`              | `[-saver\|-addonsaver\|-splash\|-type]`                                          |
| `set`                   | `<value>`                                                                        |
| `setrange`              | `<value> [value2] [value3] [...]`                                                |
| `sftp`                  | `[server]`                                                                       |
| `shownotifs`            |                                                                                  |
| `showtd`                |                                                                                  |
| `showtdzone`            | `[-all] [-selection] <timezone>`                                                 |
| `shutdown`              | `[ip] [port]`                                                                    |
| `sleep`                 | `<ms>`                                                                           |
| `sshell`                | `<address:port> <username>`                                                      |
| `sshcmd`                | `<address:port> <username> <command>`                                            |
| `sudo`                  | `<command>`                                                                      |
| `sumfile`               | `[-relative] <algorithm/all> <file> [output]`                                    |
| `sumfiles`              | `[-relative] <algorithm/all> <dir> [output]`                                     |
| `taskman`               |                                                                                  |
| `themeprev`             | `[theme]`                                                                        |
| `themeset`              | `[-y] [theme]`                                                                   |
| `unblockdbgdev`         | `<address>`                                                                      |
| `unset`                 | `[-justwipe] <$variable>`                                                        |
| `unzip`                 | `[-createdir] <zipfile> [path]`                                                  |
| `update`                |                                                                                  |
| `uptime`                |                                                                                  |
| `usermanual`            |                                                                                  |
| `verify`                | `<algorithm> <calculatedhash> <hashfile/expectedhash> <file>`                    |
| `version`               | `[-m\|-k]`                                                                       |
| `whoami`                |                                                                                  |
| `winelevate`            |                                                                                  |
| `wraptext`              | `[-columns=num] <file>`                                                          |
| `zip`                   | `[-fast\|-nocomp] [-nobasedir] <zipfile> <path>`                                 |

## Unified commands

The below commands are available to all the shells, either built-in or your custom shells:

| Commands        | Arguments and Switches                                       |
| --------------- | ------------------------------------------------------------ |
| `exec`          | `[-forked] <process> [args]`                                 |
| `exit`          |                                                              |
| `help`          | `[-general\|-mod\|-alias\|-addon\|-unified\|-all] [command]` |
| `loadhistories` |                                                              |
| `presets`       |                                                              |
| `repeat`        | `<times> [command]`                                          |
| `savehistories` |                                                              |
| `tip`           |                                                              |
| `wrap`          | `<command>`                                                  |

## Other shells

In addition to the built-in commands, we also have commands for other shells.

### Admin shell

This shell provides you administrative tools. The following commands are available:

| Commands           | Arguments and Switches                           |
| ------------------ | ------------------------------------------------ |
| `arghelp`          | `[argument]`                                     |
| `bootlog`          |                                                  |
| `cdbglog`          |                                                  |
| `clearfiredevents` |                                                  |
| `journal`          |                                                  |
| `lsevents`         |                                                  |
| `lsusers`          |                                                  |
| `userflag`         | `<user> <admin/anonymous/disabled> <false/true>` |
| `userinfo`         | `[user]`                                         |
| `userlang`         | `<user> <lang/clear>`                            |

### Debug shell

This shell provides debug information. Here are the currently supported commands:

| Commands    | Arguments and Switches |
| ----------- | ---------------------- |
| `currentbt` |                        |
| `debuglog`  | `<sessionnum>`         |
| `excinfo`   | `<excnum>`             |
| `keyinfo`   |                        |
| `lsaddons`  |                        |
| `lsshells`  |                        |
| `threadsbt` |                        |

### Hex Shell

The hex shell allows you to edit files byte by byte. You can use the following commands:

| Commands     | Arguments and Switches         |
| ------------ | ------------------------------ |
| `addbyte`    | `<byte>`                       |
| `addbytes`   |                                |
| `clear`      |                                |
| `delbyte`    | `<bytenumber>`                 |
| `delbytes`   | `<startbyte> [endbyte]`        |
| `exitnosave` |                                |
| `print`      | `[startbyte] [endbyte]`        |
| `querybyte`  | `<byte> [startbyte] [endbyte]` |
| `replace`    | `<byte> <replacedbyte>`        |
| `save`       |                                |

### JSON Shell

The JSON shell allows you to easily edit JSON files. You can use the below commands:

| Commands           | Arguments and Switches                                       |
| ------------------ | ------------------------------------------------------------ |
| `addarray`         | `[-parentproperty] <propname> <propname1> [propname2] [...]` |
| `addproperty`      | `[-parentproperty] <propname> <propvalue>`                   |
| `addobject`        | `[-parentproperty] <arrname> <arrvalue>`                     |
| `addobjectindexed` | `[-parentproperty] <idx> <arrvalue>`                         |
| `clear`            |                                                              |
| `delproperty`      | `<propname>`                                                 |
| `exitnosave`       |                                                              |
| `findproperty`     | `[-parentproperty] <propname>`                               |
| `jsoninfo`         | `[-simplified] [-showvals]`                                  |
| `print`            | `[propname]`                                                 |
| `rmobject`         | `[-parentproperty] <objname>`                                |
| `rmobjectindexed`  | `[-parentproperty] <objidx>`                                 |
| `save`             | `[-b\|-m]`                                                   |

### SQL Shell

This shell allows you to execute commands from the connected SQLite database file. You can use the below commands:

| Commands | Arguments and Switches |
| -------- | ---------------------- |
| `cmd`    | `<query>`              |
| `dbinfo` |                        |

### Text Shell

The text editor shell allows you to easily manipulate with the text files. You can use the below commands:

| Commands             | Arguments and Switches                                 |
| -------------------- | ------------------------------------------------------ |
| `addline`            | `<text>`                                               |
| `addlines`           |                                                        |
| `clear`              |                                                        |
| `delcharnum`         | `<charnum> <linenum>`                                  |
| `delline`            | `<linenum> [linenum2]`                                 |
| `delword`            | `<word/phrase> <linenum> [linenum2]`                   |
| `editline`           | `<linenum>`                                            |
| `exitnosave`         |                                                        |
| `print`              | `[linenum] [linenum2]`                                 |
| `querychar`          | `<char> <linenum/all> [linenum2]`                      |
| `queryword`          | `<word/phrase> <linenum/all> [linenum2]`               |
| `querywordregex`     | `<regex> <linenum/all> [linenum2]`                     |
| `replace`            | `<word/phrase> <word/phrase>`                          |
| `replaceinline`      | `<word/phrase> <word/phrase> <linenum/all> [linenum2]` |
| `replaceregex`       | `<regex> <word/phrase>`                                |
| `replaceinlineregex` | `<regex> <word/phrase> <linenum/all> [linenum2]`       |
| `save`               |                                                        |

## Addon commands

Additionally, addons provide commands that you can use to get the most out of them. They are available as part of the Extras addon.

### Amusements

Amusements addon provides you with a pack of games and amusements. You can use the below commands:

| Commands     | Arguments and Switches   |
| ------------ | ------------------------ |
| `backrace`   |                          |
| `hangman`    | `[-hardcore\|-practice]` |
| `meteor`     |                          |
| `quote`      |                          |
| `roulette`   |                          |
| `shipduet`   |                          |
| `snaker`     |                          |
| `solver`     |                          |
| `speedpress` | `[-e\|-m\|-h\|-v\|-c]`   |
| `wordle`     | `[-orig]`                |

### Archive shell

This addon includes an archive shell which lets you manipulate with the archive files. On startup, the below commands are added to the UESH shell:

| Commands  | Arguments and Switches |
| --------- | ---------------------- |
| `archive` | `<archivefile>`        |

Once you enter the archive shell with the provided archive file path, you can access the below archive shell commands:

| Commands | Arguments and Switches        |
| -------- | ----------------------------- |
| `cdir`   |                               |
| `chdir`  | `<directory>`                 |
| `chadir` | `<archivedir>`                |
| `get`    | `[-absolute] <entry> [where]` |
| `list`   | `[directory]`                 |
| `pack`   | `<localfile> [where]`         |

### BassBoom Addon

This addon allows you to get access to the BassBoom utility features. Please note that playing sound is not implemented yet until the migration to .NET 8.0 is done. You can use the following commands:

| Commands     | Arguments and Switches |
| ------------ | ---------------------- |
| `lyriclines` | `<lyric.lrc>`          |
| `playlyric`  | `<lyric.lrc>`          |
| `playsound`  | `<musicfile>`          |

### Caffeine Addon

This addon lets you be alarmed when your cup of tea or coffee is ready. You can use the following commands:

| Commands   | Arguments and Switches |
| ---------- | ---------------------- |
| `caffeine` | `<seconds>`            |

### Calculators Addon

This addon lets you use different calculators. Use the following commands to get started:

| Commands    | Arguments and Switches |
| ----------- | ---------------------- |
| `calc`      | `<expression>`         |
| `imaginary` | `<real> <imaginary>`   |

### Calendar Addon

This addon allows you access to the calendar functions. You can use the below commands:

| Commands   | Arguments and Switches                   |
| ---------- | ---------------------------------------- |
| `altdate`  | `[-date\|-time\|-full] [-utc] <culture>` |
| `calendar` | `<show> [-calendar=type] [year] [month]` |
|            | `<event> <add> <date> <title>`           |
|            | `<event> <remove> <eventid>`             |
|            | `<event> <list>`                         |
|            | `<event> <saveall>`                      |
|            | `<reminder> <add> <dateandtime> <title>` |
|            | `<reminder> <remove> <reminderid>`       |
|            | `<reminder> <list>`                      |
|            | `<reminder> <saveall>`                   |

### Color Conversion

This addon gives you various color model translation commands. You can use the following commands:

| Commands           | Arguments and Switches |
| ------------------ | ---------------------- |
| `colorhextorgb`    | `<#RRGGBB>`            |
| `colorhextorgbks`  | `<#RRGGBB>`            |
| `colorhextocmyk`   | `<#RRGGBB>`            |
| `colorhextocmykks` | `<#RRGGBB>`            |
| `colorhextohsl`    | `<#RRGGBB>`            |
| `colorhextohslks`  | `<#RRGGBB>`            |
| `colorrgbtohex`    | `<R> <G> <B>`          |
| `colorrgbtocmyk`   | `<R> <G> <B>`          |
| `colorrgbtocmykks` | `<R> <G> <B>`          |
| `colorrgbtohsl`    | `<R> <G> <B>`          |
| `colorrgbtohslks`  | `<R> <G> <B>`          |
| `colorhsltohex`    | `<H> <S> <L>`          |
| `colorhsltocmyk`   | `<H> <S> <L>`          |
| `colorhsltocmykks` | `<H> <S> <L>`          |
| `colorhsltorgb`    | `<H> <S> <L>`          |
| `colorhsltorgbks`  | `<H> <S> <L>`          |
| `colorcmyktohex`   | `<C> <M> <Y> <K>`      |
| `colorcmyktorgb`   | `<C> <M> <Y> <K>`      |
| `colorcmyktorgbks` | `<C> <M> <Y> <K>`      |
| `colorcmyktohsl`   | `<C> <M> <Y> <K>`      |
| `colorcmyktohslks` | `<C> <M> <Y> <K>`      |

### Contacts

You can use the following commands provided by the contacts addon:

| Commands   | Arguments and Switches |
| ---------- | ---------------------- |
| `contacts` |                        |

### Dictionary

You can use the following commands provided by the dictionary addon:

| Commands | Arguments and Switches |
| -------- | ---------------------- |
| `dict`   | `<word>`               |

### Forecast

The forecast addon allows you to take a look at the current forecast across the world. You can use the following commands:

| Commands  | Arguments and Switches               |
| --------- | ------------------------------------ |
| `weather` | `[-list] <cityid/cityname> [apikey]` |

### FTP Shell

This shell provides you a client to the FTP servers. Here is a list of supported commands:

| Commands    | Arguments and Switches                   |
| ----------- | ---------------------------------------- |
| `cat`       | `<file>`                                 |
| `cdl`       | `<directory>`                            |
| `cdr`       | `<directory>`                            |
| `cp`        | `<source> <target>`                      |
| `del`       | `<file>`                                 |
| `detach`    |                                          |
| `execute`   | `<command>`                              |
| `get`       | `<file> [where]`                         |
| `getfolder` | `<folder> [where]`                       |
| `info`      |                                          |
| `lsl`       | `[-showdetails\|suppressmessages] [dir]` |
| `lsr`       | `[-showdetails] [dir]`                   |
| `mv`        | `<source> <target>`                      |
| `put`       | `<file> [output]`                        |
| `putfolder` | `<folder> [output]`                      |
| `pwdl`      |                                          |
| `pwdr`      |                                          |
| `perm`      | `<file> <permnum>`                       |
| `sumfile`   | `<file> <algorithm>`                     |
| `sumfiles`  | `<directory> <algorithm>`                |
| `type`      | `<a/b>`                                  |

### Git Shell

This addon includes a Git shell which lets you practice version controlling. On startup, the below commands are added to the UESH shell:

| Commands | Arguments and Switches |
| -------- | ---------------------- |
| `gitsh`  | `<repopath>`           |

Once you enter the Git shell with the provided repo path, you can access the below archive shell commands:

| Commands     | Arguments and Switches   |
| ------------ | ------------------------ |
| `blame`      |                          |
| `checkout`   | `<branch>`               |
| `commit`     | `<summary>`              |
| `describe`   | `<commitsha>`            |
| `fetch`      | `[remote]`               |
| `filestatus` | `<file>`                 |
| `info`       |                          |
| `lsbranches` |                          |
| `lscommits`  |                          |
| `lsremotes`  |                          |
| `lstags`     |                          |
| `maketag`    | `<tagname> [message]`    |
| `pull`       |                          |
| `push`       |                          |
| `reset`      | `[-soft\|-hard\|-mixed]` |
| `setid`      | `<email> <username>`     |
| `stage`      | `<unstagedfile>`         |
| `stageall`   |                          |
| `status`     |                          |
| `unstage`    | `<stagedfile>`           |
| `unstageall` |                          |

### HTTP Shell

The HTTP shell allows you to interact with an HTTP server, like sending requests to it. You can use the below commands:

| Commands     | Arguments and Switches   |
| ------------ | ------------------------ |
| `addheader`  | `<key> <value>`          |
| `curragent`  |                          |
| `delete`     | `<request>`              |
| `detach`     |                          |
| `editheader` | `<key> <value>`          |
| `get`        | `<request>`              |
| `getstring`  | `<request>`              |
| `lsheader`   |                          |
| `put`        | `<request> <pathtofile>` |
| `putstring`  | `<request> <string>`     |
| `post`       | `<request> <pathtofile>` |
| `poststring` | `<request> <string>`     |
| `rmheader`   | `<key>`                  |
| `setagent`   | `<useragent>`            |

### Internet Radio

You can use the following commands to get information about your Internet radio station:

| Commands    | Arguments and Switches        |
| ----------- | ----------------------------- |
| `netfminfo` | `[-secure] <hostname> <port>` |

### Language Studio

You can use the following commands to build your own language:

| Commands | Arguments and Switches |
| -------- | ---------------------- |
| `mklang` | `<pathtotranslations>` |

### Name generator

You can generate names by using the following commands:

| Commands        | Arguments and Switches                                                        |
| --------------- | ----------------------------------------------------------------------------- |
| `findfirstname` | `[-t] [term] [nameprefix] [namesuffix]`                                       |
| `findsurname`   | `[term] [surnameprefix] [surnamesuffix]`                                      |
| `genname`       | `[-t] <namescount> [nameprefix] [namesuffix] [surnameprefix] [surnamesuffix]` |

### Mail Shell

This shell allows you to check your e-mails and send them. You can use the following commands:

| Commands  | Arguments and Switches            |
| --------- | --------------------------------- |
| `cd`      | `<folder>`                        |
| `detach`  |                                   |
| `lsdirs`  |                                   |
| `list`    | `[pagenum]`                       |
| `mkdir`   | `<foldername>`                    |
| `mv`      | `<mailid> <targetfolder>`         |
| `mvall`   | `<sendername> <targetfolder>`     |
| `read`    | `<mailid>`                        |
| `readenc` | `<mailid>`                        |
| `ren`     | `<oldfoldername> <newfoldername>` |
| `rm`      | `<mailid>`                        |
| `rmall`   | `<sendername>`                    |
| `rmdir`   | `<foldername>`                    |
| `send`    |                                   |
| `sendenc` |                                   |

### RSS Shell

You can use this shell to read your RSS feeds. You can use the below commands:

| Commands       | Arguments and Switches       |
| -------------- | ---------------------------- |
| `articleinfo`  | `<feednum>`                  |
| `bookmark`     |                              |
| `detach`       |                              |
| `feedinfo`     |                              |
| `list`         |                              |
| `listbookmark` |                              |
| `read`         | `<feednum>`                  |
| `search`       | `[-t\|-d\|-a\|-cs] <phrase>` |
| `unbookmark`   |                              |

### SFTP Shell

SFTP shell allows you to interact with the SFTP servers.

| Commands | Arguments and Switches                    |
| -------- | ----------------------------------------- |
| `cat`    | `<file>`                                  |
| `cdl`    | `<dir>`                                   |
| `cdr`    | `<dir>`                                   |
| `del`    | `<file>`                                  |
| `detach` |                                           |
| `get`    | `<file>`                                  |
| `lsl`    | `[-showdetails\|-suppressmessages] [dir]` |
| `lsr`    | `[-showdetails] [dir]`                    |
| `put`    | `<file>`                                  |
| `pwdl`   |                                           |
| `pwdr`   |                                           |

### Notes

You can jot down notes by using the following commands:

| Commands      | Arguments and Switches |
| ------------- | ---------------------- |
| `addnote`     | `<contents>`           |
| `listnotes`   |                        |
| `reloadnotes` |                        |
| `removenote`  | `<notenum>`            |
| `removenotes` |                        |
| `savenotes`   |                        |

### Theme Studio

You can make your own precious and epic themes by using the following commands:

| Commands  | Arguments and Switches |
| --------- | ---------------------- |
| `mktheme` | `<themename>`          |

### Time info

You can get detailed time info by using the following commands:

| Commands      | Arguments and Switches |
| ------------- | ---------------------- |
| `gettimeinfo` | `[-now] <date>`        |

### Timers

You can use the timer and the stopwatch using the following commands:

| Commands    | Arguments and Switches |
| ----------- | ---------------------- |
| `stopwatch` |                        |
| `timer`     |                        |

### To-do List

You can build your own task list using the following commands:

| Commands | Arguments and Switches |
| -------- | ---------------------- |
| `todo`   | `<add> <taskname>`     |
|          | `<remove> <taskname>`  |
|          | `<done> <taskname>`    |
|          | `<undone> <taskname>`  |
|          | `<list>`               |
|          | `<save>`               |
|          | `<load>`               |

### Unit conversion

You can initiate unit conversion using the following commands:

| Commands    | Arguments and Switches                                   |
| ----------- | -------------------------------------------------------- |
| `listunits` | `<type>`                                                 |
| `unitconv`  | `[-tui] <unittype> <quantity> <sourceunit> <targetunit>` |
