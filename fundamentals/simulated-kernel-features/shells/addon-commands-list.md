---
description: List of available addon commands
icon: square-code
---

# Addon Commands List

This page is a reference that serves as a list of available addon commands.

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
| `2018`       |                          |

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

This addon allows you to get access to the BassBoom utility features. You can use the following commands:

| Commands      | Arguments and Switches |
| ------------- | ---------------------- |
| `lyriclines`  | `<lyric.lrc>`          |
| `playlyric`   | `<lyric.lrc>`          |
| `playsound`   | `<musicfile>`          |
| `musicplayer` | `[musicfile]`          |

### Caffeine Addon

This addon lets you be alarmed when your cup of tea or coffee is ready. You can use the following commands:

| Commands   | Arguments and Switches |
| ---------- | ---------------------- |
| `caffeine` | `[-abort] <seconds>`   |

### Calculators Addon

This addon lets you use different calculators. Use the following commands to get started:

| Commands    | Arguments and Switches |
| ----------- | ---------------------- |
| `calc`      | `<expression>`         |
| `imaginary` | `<real> <imaginary>`   |

### Calendar Addon

This addon allows you access to the calendar functions. You can use the below commands:

| Commands   | Arguments and Switches                            |
| ---------- | ------------------------------------------------- |
| `altdate`  | `[-date\|-time\|-full] [-utc] <culture>`          |
| `calendar` | `<tui> [-calendar=type] [-legacy] [year] [month]` |
|            | `<event> <add> <date> <title>`                    |
|            | `<event> <remove> <eventid>`                      |
|            | `<event> <list>`                                  |
|            | `<event> <saveall>`                               |
|            | `<reminder> <add> <dateandtime> <title>`          |
|            | `<reminder> <remove> <reminderid>`                |
|            | `<reminder> <list>`                               |
|            | `<reminder> <saveall>`                            |

### Color Conversion

This addon gives you various color model translation commands. You can use the following commands:

| Commands           | Arguments and Switches |
| ------------------ | ---------------------- |
| `colorhextorgb`    | `<#RRGGBB>`            |
| `colorhextorgbks`  | `<#RRGGBB>`            |
| `colorhextocmyk`   | `<#RRGGBB>`            |
| `colorhextocmykks` | `<#RRGGBB>`            |
| `colorhextocmy`    | `<#RRGGBB>`            |
| `colorhextocmyks`  | `<#RRGGBB>`            |
| `colorhextohsv`    | `<#RRGGBB>`            |
| `colorhextohsvks`  | `<#RRGGBB>`            |
| `colorhextohsl`    | `<#RRGGBB>`            |
| `colorhextohslks`  | `<#RRGGBB>`            |
| `colorhextoryb`    | `<#RRGGBB>`            |
| `colorhextorybks`  | `<#RRGGBB>`            |
| `colorhextoyiq`    | `<#RRGGBB>`            |
| `colorhextoyiqks`  | `<#RRGGBB>`            |
| `colorhextoyuv`    | `<#RRGGBB>`            |
| `colorhextoyuvks`  | `<#RRGGBB>`            |
| `colorrgbtohex`    | `<R> <G> <B>`          |
| `colorrgbtocmyk`   | `<R> <G> <B>`          |
| `colorrgbtocmykks` | `<R> <G> <B>`          |
| `colorrgbtocmy`    | `<R> <G> <B>`          |
| `colorrgbtocmyks`  | `<R> <G> <B>`          |
| `colorrgbtohsv`    | `<R> <G> <B>`          |
| `colorrgbtohsvks`  | `<R> <G> <B>`          |
| `colorrgbtohsl`    | `<R> <G> <B>`          |
| `colorrgbtohslks`  | `<R> <G> <B>`          |
| `colorrgbtoryb`    | `<R> <G> <B>`          |
| `colorrgbtorybks`  | `<R> <G> <B>`          |
| `colorrgbtoyiq`    | `<R> <G> <B>`          |
| `colorrgbtoyiqks`  | `<R> <G> <B>`          |
| `colorrgbtoyuv`    | `<R> <G> <B>`          |
| `colorrgbtoyuvks`  | `<R> <G> <B>`          |
| `colorrybtorgb`    | `<R> <Y> <B>`          |
| `colorrybtocmyk`   | `<R> <Y> <B>`          |
| `colorrybtocmykks` | `<R> <Y> <B>`          |
| `colorrybtocmy`    | `<R> <Y> <B>`          |
| `colorrybtocmyks`  | `<R> <Y> <B>`          |
| `colorrybtohsv`    | `<R> <Y> <B>`          |
| `colorrybtohsvks`  | `<R> <Y> <B>`          |
| `colorrybtohsl`    | `<R> <Y> <B>`          |
| `colorrybtohslks`  | `<R> <Y> <B>`          |
| `colorrybtorgb`    | `<R> <Y> <B>`          |
| `colorrybtorgbks`  | `<R> <Y> <B>`          |
| `colorrybtoyiq`    | `<R> <Y> <B>`          |
| `colorrybtoyiqks`  | `<R> <Y> <B>`          |
| `colorrybtoyuv`    | `<R> <Y> <B>`          |
| `colorrybtoyuvks`  | `<R> <Y> <B>`          |
| `colorhsltohex`    | `<H> <S> <L>`          |
| `colorhsltocmyk`   | `<H> <S> <L>`          |
| `colorhsltocmykks` | `<H> <S> <L>`          |
| `colorhsltocmy`    | `<H> <S> <L>`          |
| `colorhsltocmyks`  | `<H> <S> <L>`          |
| `colorhsltoryb`    | `<H> <S> <L>`          |
| `colorhsltorybks`  | `<H> <S> <L>`          |
| `colorhsltorgb`    | `<H> <S> <L>`          |
| `colorhsltorgbks`  | `<H> <S> <L>`          |
| `colorhsltoryb`    | `<H> <S> <L>`          |
| `colorhsltorybks`  | `<H> <S> <L>`          |
| `colorhsltoyiq`    | `<H> <S> <L>`          |
| `colorhsltoyiqks`  | `<H> <S> <L>`          |
| `colorhsltoyuv`    | `<H> <S> <L>`          |
| `colorhsltoyuvks`  | `<H> <S> <L>`          |
| `colorhsvtohex`    | `<H> <S> <V>`          |
| `colorhsvtocmyk`   | `<H> <S> <V>`          |
| `colorhsvtocmykks` | `<H> <S> <V>`          |
| `colorhsvtocmy`    | `<H> <S> <V>`          |
| `colorhsvtocmyks`  | `<H> <S> <V>`          |
| `colorhsvtohsl`    | `<H> <S> <V>`          |
| `colorhsvtohslks`  | `<H> <S> <V>`          |
| `colorhsvtorgb`    | `<H> <S> <V>`          |
| `colorhsvtorgbks`  | `<H> <S> <V>`          |
| `colorhsvtoryb`    | `<H> <S> <V>`          |
| `colorhsvtorybks`  | `<H> <S> <V>`          |
| `colorhsvtoyiq`    | `<H> <S> <V>`          |
| `colorhsvtoyiqks`  | `<H> <S> <V>`          |
| `colorhsvtoyuv`    | `<H> <S> <V>`          |
| `colorhsvtoyuvks`  | `<H> <S> <V>`          |
| `colorcmyktohex`   | `<C> <M> <Y> <K>`      |
| `colorcmyktorgb`   | `<C> <M> <Y> <K>`      |
| `colorcmyktorgbks` | `<C> <M> <Y> <K>`      |
| `colorcmyktoryb`   | `<C> <M> <Y> <K>`      |
| `colorcmyktorybks` | `<C> <M> <Y> <K>`      |
| `colorcmyktohsv`   | `<C> <M> <Y> <K>`      |
| `colorcmyktohsvks` | `<C> <M> <Y> <K>`      |
| `colorcmyktohsl`   | `<C> <M> <Y> <K>`      |
| `colorcmyktohslks` | `<C> <M> <Y> <K>`      |
| `colorcmyktocmy`   | `<C> <M> <Y> <K>`      |
| `colorcmyktocmyks` | `<C> <M> <Y> <K>`      |
| `colorcmyktoyiq`   | `<C> <M> <Y> <K>`      |
| `colorcmyktoyiqks` | `<C> <M> <Y> <K>`      |
| `colorcmyktoyuv`   | `<C> <M> <Y> <K>`      |
| `colorcmyktoyuvks` | `<C> <M> <Y> <K>`      |
| `colorcmytohex`    | `<C> <M> <Y>`          |
| `colorcmytorgb`    | `<C> <M> <Y>`          |
| `colorcmytorgbks`  | `<C> <M> <Y>`          |
| `colorcmytoryb`    | `<C> <M> <Y>`          |
| `colorcmytorybks`  | `<C> <M> <Y>`          |
| `colorcmytohsl`    | `<C> <M> <Y>`          |
| `colorcmytohslks`  | `<C> <M> <Y>`          |
| `colorcmytohsv`    | `<C> <M> <Y>`          |
| `colorcmytohsvks`  | `<C> <M> <Y>`          |
| `colorcmytocmyk`   | `<C> <M> <Y>`          |
| `colorcmytocmykks` | `<C> <M> <Y>`          |
| `colorcmytoyiq`    | `<C> <M> <Y>`          |
| `colorcmytoyiqks`  | `<C> <M> <Y>`          |
| `colorcmytoyuv`    | `<C> <M> <Y>`          |
| `colorcmytoyuvks`  | `<C> <M> <Y>`          |
| `coloryiqtohex`    | `<Y> <I> <Q>`          |
| `coloryiqtorgb`    | `<Y> <I> <Q>`          |
| `coloryiqtorgbks`  | `<Y> <I> <Q>`          |
| `coloryiqtoryb`    | `<Y> <I> <Q>`          |
| `coloryiqtorybks`  | `<Y> <I> <Q>`          |
| `coloryiqtocmyk`   | `<Y> <I> <Q>`          |
| `coloryiqtocmykks` | `<Y> <I> <Q>`          |
| `coloryiqtocmy`    | `<Y> <I> <Q>`          |
| `coloryiqtocmyks`  | `<Y> <I> <Q>`          |
| `coloryiqtohsl`    | `<Y> <I> <Q>`          |
| `coloryiqtohslks`  | `<Y> <I> <Q>`          |
| `coloryiqtohsv`    | `<Y> <I> <Q>`          |
| `coloryiqtohsvks`  | `<Y> <I> <Q>`          |
| `coloryiqtoyuv`    | `<Y> <I> <Q>`          |
| `coloryiqtoyuvks`  | `<Y> <I> <Q>`          |
| `coloryuvtohex`    | `<Y> <U> <V>`          |
| `coloryuvtorgb`    | `<Y> <U> <V>`          |
| `coloryuvtorgbks`  | `<Y> <U> <V>`          |
| `coloryuvtoryb`    | `<Y> <U> <V>`          |
| `coloryuvtorybks`  | `<Y> <U> <V>`          |
| `coloryuvtocmyk`   | `<Y> <U> <V>`          |
| `coloryuvtocmykks` | `<Y> <U> <V>`          |
| `coloryuvtocmy`    | `<Y> <U> <V>`          |
| `coloryuvtocmyks`  | `<Y> <U> <V>`          |
| `coloryuvtohsl`    | `<Y> <U> <V>`          |
| `coloryuvtohslks`  | `<Y> <U> <V>`          |
| `coloryuvtohsv`    | `<Y> <U> <V>`          |
| `coloryuvtohsvks`  | `<Y> <U> <V>`          |
| `coloryuvtoyiq`    | `<Y> <U> <V>`          |
| `coloryuvtoyiqks`  | `<Y> <U> <V>`          |

### Contacts

You can use the following commands provided by the contacts addon:

| Commands   | Arguments and Switches |
| ---------- | ---------------------- |
| `contacts` |                        |

### Diagnostics

You can use the following commands provided by the diagnostics addon:

| Commands    | Arguments and Switches |
| ----------- | ---------------------- |
| `threadsbt` |                        |

### Dictionary

You can use the following commands provided by the dictionary addon:

| Commands | Arguments and Switches |
| -------- | ---------------------- |
| `dict`   | `<word>`               |

### Docking

You can use the following commands provided by the screen docking addon:

| Commands | Arguments and Switches |
| -------- | ---------------------- |
| `dock`   | `<dockId>`             |

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
| `diff`       | `[-tree\|-patch\|-all]`  |
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

### HDD Uncleaner 2015 Addon

This addon is a Legacy addon that shows you a mock-up of our ancient app, HDD Cleaner 2015. You can use the below commands:

| Commands | Arguments and Switches |
| -------- | ---------------------- |
| `2015`   |                        |

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

### JSON Shell

The JSON shell allows you to easily edit JSON files. You can use the below commands:

| Commands       | Arguments and Switches                                            |
| -------------- | ----------------------------------------------------------------- |
| `add`          | `<-type=value> [-parentPath=value] [-propName=value] <jsonValue>` |
| `clear`        |                                                                   |
| `exitnosave`   |                                                                   |
| `findproperty` | `[-parentproperty] <propname>`                                    |
| `jsoninfo`     | `[-simplified] [-showvals]`                                       |
| `jsonminify`   | `<jsonfile> <output>`                                             |
| `jsonbeautify` | `<jsonfile> <output>`                                             |
| `jsondiff`     | `<file1> <file2>`                                                 |
| `print`        | `[propname]`                                                      |
| `rm`           | `<objectPath>`                                                    |
| `save`         | `[-b\|-m]`                                                        |
| `set`          | `<-type=value> [-parentPath=value] [-propName=value] <jsonValue>` |
| `tui`          |                                                                   |

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

You can use this shell to read your RSS feeds using the `rss` command. You can use the below commands:

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
| `notestui`    |                        |
| `reloadnotes` |                        |
| `removenote`  | `<notenum>`            |
| `removenotes` |                        |
| `savenotes`   |                        |

### SQL Shell

This shell allows you to execute commands from the connected SQLite database file. You can use the below commands:

| Commands | Arguments and Switches |
| -------- | ---------------------- |
| `cmd`    | `<query>`              |
| `dbinfo` |                        |
| `tui`    |                        |

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
