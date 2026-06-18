---
description: List of available addon commands
icon: square-code
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/fundamentals/simulated-kernel-features/shells/addon-commands-list
---

# Addon Commands List

This page is a reference that serves as a list of available addon commands.

***

## <mark style="color:$primary;">Addon commands</mark>

Additionally, addons provide commands that you can use to get the most out of them. They are available as part of the Extras addon.

<details>

<summary>Amusements</summary>

Amusements addon provides you with a pack of games and amusements. You can use the below commands:

<table><thead><tr><th width="130.6614990234375">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>backrace</code></td><td></td></tr><tr><td><code>hangman</code></td><td><code>[-uncommon|-common] [-hardcore|-practice]</code></td></tr><tr><td><code>meteor</code></td><td></td></tr><tr><td><code>pong</code></td><td></td></tr><tr><td><code>quote</code></td><td></td></tr><tr><td><code>roulette</code></td><td></td></tr><tr><td><code>shipduet</code></td><td></td></tr><tr><td><code>snaker</code></td><td></td></tr><tr><td><code>solver</code></td><td></td></tr><tr><td><code>speedpress</code></td><td><code>[-e|-m|-h|-v|-c]</code></td></tr><tr><td><code>wordle</code></td><td><code>[-uncommon|-common] [-orig]</code></td></tr></tbody></table>

</details>

<details>

<summary>Archive shell</summary>

This addon includes an archive shell which lets you manipulate with the archive files. On startup, the below commands are added to the UESH shell:

<table><thead><tr><th width="129.9947509765625">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>archive</code></td><td><code>&#x3C;archivefile></code></td></tr></tbody></table>

Once you enter the archive shell with the provided archive file path, you can access the below archive shell commands:

<table><thead><tr><th width="129.99481201171875">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>cdir</code></td><td></td></tr><tr><td><code>chdir</code></td><td><code>&#x3C;directory></code></td></tr><tr><td><code>chadir</code></td><td><code>&#x3C;archivedir></code></td></tr><tr><td><code>get</code></td><td><code>[-absolute] &#x3C;entry> [where]</code></td></tr><tr><td><code>list</code></td><td><code>[directory]</code></td></tr><tr><td><code>pack</code></td><td><code>&#x3C;localfile> [where]</code></td></tr></tbody></table>

</details>

<details>

<summary>BassBoom Addon</summary>

This addon allows you to get access to the BassBoom utility features. You can use the following commands:

<table><thead><tr><th width="129.9947509765625">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>lyriclines</code></td><td><code>&#x3C;lyric.lrc></code></td></tr><tr><td><code>playlyric</code></td><td><code>&#x3C;lyric.lrc></code></td></tr><tr><td><code>playsound</code></td><td><code>&#x3C;musicfile></code></td></tr><tr><td><code>netfminfo</code></td><td><code>[-secure] &#x3C;hostname> &#x3C;port></code></td></tr></tbody></table>

</details>

<details>

<summary>Beep Synth Addon</summary>

This addon allows you to play beep synth files using the following commands:

<table><thead><tr><th width="131.328125">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>beepsynth</code></td><td><code>&#x3C;synthfile></code></td></tr></tbody></table>

</details>

<details>

<summary>Caffeine Addon</summary>

This addon lets you be alarmed when your cup of tea or coffee is ready. You can use the following commands:

<table><thead><tr><th width="129.9947509765625">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>caffeine</code></td><td><code>[-abort] &#x3C;seconds></code></td></tr></tbody></table>

</details>

<details>

<summary>Calculators Addon</summary>

This addon lets you use different calculators. Use the following commands to get started:

<table><thead><tr><th width="129.328125">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>calc</code></td><td><code>&#x3C;expression></code></td></tr><tr><td><code>imaginary</code></td><td><code>&#x3C;real> &#x3C;imaginary></code></td></tr></tbody></table>

</details>

<details>

<summary>Calendar Addon</summary>

This addon allows you access to the calendar functions. You can use the below commands:

<table><thead><tr><th width="129.328125">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>altdate</code></td><td><code>[-date|-time|-full] [-utc] &#x3C;culture></code></td></tr><tr><td><code>calendar</code></td><td><code>&#x3C;tui> [-calendar=type] [-legacy] [year] [month]</code></td></tr><tr><td></td><td><code>&#x3C;event> &#x3C;add> &#x3C;date> &#x3C;title></code></td></tr><tr><td></td><td><code>&#x3C;event> &#x3C;remove> &#x3C;eventid></code></td></tr><tr><td></td><td><code>&#x3C;event> &#x3C;list></code></td></tr><tr><td></td><td><code>&#x3C;event> &#x3C;saveall></code></td></tr><tr><td></td><td><code>&#x3C;reminder> &#x3C;add> &#x3C;dateandtime> &#x3C;title></code></td></tr><tr><td></td><td><code>&#x3C;reminder> &#x3C;remove> &#x3C;reminderid></code></td></tr><tr><td></td><td><code>&#x3C;reminder> &#x3C;list></code></td></tr><tr><td></td><td><code>&#x3C;reminder> &#x3C;saveall></code></td></tr></tbody></table>

</details>

<details>

<summary>Chatbot AI</summary>

This addon gives you commands that allow you to interact with the chatbot powered by ChatGPT. You can use the following commands:

<table><thead><tr><th width="129.66656494140625">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>chatbot</code></td><td><code>[-apikey=value] [-model=value]</code></td></tr></tbody></table>

</details>

<details>

<summary>Chemistry</summary>

This addon gives you commands that allow you to interact with the periodic table. You can use the following commands:

<table><thead><tr><th width="129.6666259765625">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>element</code></td><td><code>name/symbol/atomicNumber</code></td></tr><tr><td><code>elements</code></td><td></td></tr></tbody></table>

</details>

<details>

<summary>Color Conversion</summary>

This addon gives you various color model translation commands. You can use the following commands:

<table><thead><tr><th width="161.328125">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>colorspecto</code></td><td><code>&#x3C;targetModelName> &#x3C;specifier></code></td></tr><tr><td><code>colorspectohex</code></td><td><code>&#x3C;specifier></code></td></tr><tr><td><code>colorspectoks</code></td><td><code>&#x3C;targetModelName> &#x3C;specifier></code></td></tr><tr><td><code>colorto</code></td><td><code>&#x3C;sourceModelName> &#x3C;targetModelName> &#x3C;number1> &#x3C;number2> &#x3C;number3> [number4]</code></td></tr><tr><td><code>colortohex</code></td><td><code>&#x3C;sourceModelName> &#x3C;number1> &#x3C;number2> &#x3C;number3> [number4]</code></td></tr><tr><td><code>colortoks</code></td><td><code>&#x3C;sourceModelName> &#x3C;targetModelName> &#x3C;number1> &#x3C;number2> &#x3C;number3> [number4]</code></td></tr></tbody></table>

</details>

<details>

<summary>Contacts</summary>

You can use the following commands provided by the contacts addon:

<table><thead><tr><th width="159.99481201171875">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>contacts</code></td><td></td></tr><tr><td><code>listcontacts</code></td><td></td></tr><tr><td><code>loadcontacts</code></td><td></td></tr><tr><td><code>importcontacts</code></td><td><code>[-mecard] &#x3C;mecard/path></code></td></tr><tr><td><code>contactinfo</code></td><td><code>&#x3C;contactNum></code></td></tr></tbody></table>

</details>

<details>

<summary>Dates</summary>

You can get detailed time info, and use the timer and the stopwatch by using the following commands:

<table><thead><tr><th width="139.32806396484375">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>expiry</code></td><td><code>[-implicit] &#x3C;production> &#x3C;expiry></code></td></tr><tr><td><code>gettimeinfo</code></td><td><code>[-now] &#x3C;date></code></td></tr><tr><td><code>pomodoro</code></td><td></td></tr><tr><td><code>stopwatch</code></td><td></td></tr><tr><td><code>timer</code></td><td></td></tr></tbody></table>

</details>

<details>

<summary>Diagnostics</summary>

You can use the following commands provided by the diagnostics addon:

<table><thead><tr><th width="129.9947509765625">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>threadsbt</code></td><td></td></tr></tbody></table>

</details>

<details>

<summary>Dictionary</summary>

You can use the following commands provided by the dictionary addon:

<table><thead><tr><th width="130.661376953125">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>dict</code></td><td><code>&#x3C;word></code></td></tr></tbody></table>

</details>

<details>

<summary>Docking</summary>

You can use the following commands provided by the screen docking addon:

<table><thead><tr><th width="130.3333740234375">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>dock</code></td><td><code>&#x3C;dockId></code></td></tr></tbody></table>

</details>

<details>

<summary>Forecast</summary>

The forecast addon allows you to take a look at the current forecast across the world. You can use the following commands:

<table><thead><tr><th width="130.661376953125">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>weather</code></td><td><code>[-tui] [-list=name] &#x3C;latitude> &#x3C;longitude> [apikey]</code></td></tr><tr><td><code>weather-old</code></td><td><code>[-list] &#x3C;cityid/cityname> [apikey]</code></td></tr></tbody></table>

</details>

<details>

<summary>FTP Shell</summary>

This shell provides you a client to the FTP servers. You can use the following commands from MESH:

<table><thead><tr><th width="131.328125">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>ftp</code></td><td><code>[server]</code></td></tr></tbody></table>

You can use the following commands in the FTP shell:

<table><thead><tr><th width="129.9947509765625">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>cat</code></td><td><code>&#x3C;file></code></td></tr><tr><td><code>cdl</code></td><td><code>&#x3C;directory></code></td></tr><tr><td><code>cdr</code></td><td><code>&#x3C;directory></code></td></tr><tr><td><code>cp</code></td><td><code>&#x3C;source> &#x3C;target></code></td></tr><tr><td><code>del</code></td><td><code>&#x3C;file></code></td></tr><tr><td><code>detach</code></td><td></td></tr><tr><td><code>execute</code></td><td><code>&#x3C;command></code></td></tr><tr><td><code>get</code></td><td><code>&#x3C;file> [where]</code></td></tr><tr><td><code>getfolder</code></td><td><code>&#x3C;folder> [where]</code></td></tr><tr><td><code>ifm</code></td><td></td></tr><tr><td><code>info</code></td><td></td></tr><tr><td><code>lsl</code></td><td><code>[-showdetails|suppressmessages] [dir]</code></td></tr><tr><td><code>lsr</code></td><td><code>[-showdetails] [dir]</code></td></tr><tr><td><code>mkldir</code></td><td><code>&#x3C;directory></code></td></tr><tr><td><code>mkrdir</code></td><td><code>&#x3C;directory></code></td></tr><tr><td><code>mv</code></td><td><code>&#x3C;source> &#x3C;target></code></td></tr><tr><td><code>put</code></td><td><code>&#x3C;file> [output]</code></td></tr><tr><td><code>putfolder</code></td><td><code>&#x3C;folder> [output]</code></td></tr><tr><td><code>pwdl</code></td><td></td></tr><tr><td><code>pwdr</code></td><td></td></tr><tr><td><code>perm</code></td><td><code>&#x3C;file> &#x3C;permnum></code></td></tr><tr><td><code>sumfile</code></td><td><code>&#x3C;file> &#x3C;algorithm></code></td></tr><tr><td><code>sumfiles</code></td><td><code>&#x3C;directory> &#x3C;algorithm></code></td></tr><tr><td><code>type</code></td><td><code>&#x3C;a/b></code></td></tr></tbody></table>

</details>

<details>

<summary>Git Shell</summary>

This addon includes a Git shell which lets you practice version controlling. On startup, the below commands are added to the UESH shell:

<table><thead><tr><th width="129.99481201171875">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>gitsh</code></td><td><code>&#x3C;repopath></code></td></tr></tbody></table>

Once you enter the Git shell with the provided repo path, you can access the below archive shell commands:

<table><thead><tr><th width="130.66143798828125">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>blame</code></td><td></td></tr><tr><td><code>checkout</code></td><td><code>&#x3C;branch></code></td></tr><tr><td><code>commit</code></td><td><code>&#x3C;summary></code></td></tr><tr><td><code>describe</code></td><td><code>&#x3C;commitsha></code></td></tr><tr><td><code>diff</code></td><td><code>[-tree|-patch|-all]</code></td></tr><tr><td><code>fetch</code></td><td><code>[remote]</code></td></tr><tr><td><code>filestatus</code></td><td><code>&#x3C;file></code></td></tr><tr><td><code>info</code></td><td></td></tr><tr><td><code>lsbranches</code></td><td></td></tr><tr><td><code>lscommits</code></td><td></td></tr><tr><td><code>lsremotes</code></td><td></td></tr><tr><td><code>lstags</code></td><td></td></tr><tr><td><code>maketag</code></td><td><code>&#x3C;tagname> [message]</code></td></tr><tr><td><code>pull</code></td><td></td></tr><tr><td><code>push</code></td><td></td></tr><tr><td><code>reset</code></td><td><code>[-soft|-hard|-mixed]</code></td></tr><tr><td><code>setid</code></td><td><code>&#x3C;email> &#x3C;username></code></td></tr><tr><td><code>stage</code></td><td><code>&#x3C;unstagedfile></code></td></tr><tr><td><code>stageall</code></td><td></td></tr><tr><td><code>status</code></td><td></td></tr><tr><td><code>unstage</code></td><td><code>&#x3C;stagedfile></code></td></tr><tr><td><code>unstageall</code></td><td></td></tr></tbody></table>

</details>

<details>

<summary>HTTP Shell</summary>

The HTTP shell allows you to interact with an HTTP server, like sending requests to it. You can use the following commands from MESH:

<table><thead><tr><th width="130.6614990234375">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>http</code></td><td></td></tr></tbody></table>

You can use the following commands in the HTTP shell:

<table><thead><tr><th width="129.6666259765625">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>addheader</code></td><td><code>&#x3C;key> &#x3C;value></code></td></tr><tr><td><code>curragent</code></td><td></td></tr><tr><td><code>delete</code></td><td><code>&#x3C;request></code></td></tr><tr><td><code>detach</code></td><td></td></tr><tr><td><code>editheader</code></td><td><code>&#x3C;key> &#x3C;value></code></td></tr><tr><td><code>get</code></td><td><code>&#x3C;request></code></td></tr><tr><td><code>getstring</code></td><td><code>&#x3C;request></code></td></tr><tr><td><code>lsheader</code></td><td></td></tr><tr><td><code>put</code></td><td><code>&#x3C;request> &#x3C;pathtofile></code></td></tr><tr><td><code>putstring</code></td><td><code>&#x3C;request> &#x3C;string></code></td></tr><tr><td><code>post</code></td><td><code>&#x3C;request> &#x3C;pathtofile></code></td></tr><tr><td><code>poststring</code></td><td><code>&#x3C;request> &#x3C;string></code></td></tr><tr><td><code>rmheader</code></td><td><code>&#x3C;key></code></td></tr><tr><td><code>setagent</code></td><td><code>&#x3C;useragent></code></td></tr></tbody></table>

</details>

<details>

<summary>JSON Shell</summary>

The JSON shell allows you to easily edit JSON files. You can use the following commands from MESH:

<table><thead><tr><th width="141.32806396484375">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>jsonminify</code></td><td><code>&#x3C;jsonfile> &#x3C;output></code></td></tr><tr><td><code>jsonbeautify</code></td><td><code>&#x3C;jsonfile> &#x3C;output></code></td></tr><tr><td><code>jsondiff</code></td><td><code>&#x3C;file1> &#x3C;file2></code></td></tr></tbody></table>

You can use the following commands in the JSON shell:

<table><thead><tr><th width="139.328125">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>add</code></td><td><code>&#x3C;-type=value> [-parentPath=value] [-propName=value] &#x3C;jsonValue></code></td></tr><tr><td><code>clear</code></td><td></td></tr><tr><td><code>exitnosave</code></td><td></td></tr><tr><td><code>findproperty</code></td><td><code>[-parentproperty] &#x3C;propname></code></td></tr><tr><td><code>jsoninfo</code></td><td><code>[-simplified] [-showvals]</code></td></tr><tr><td><code>print</code></td><td><code>[propname]</code></td></tr><tr><td><code>rm</code></td><td><code>&#x3C;objectPath></code></td></tr><tr><td><code>save</code></td><td><code>[-b|-m]</code></td></tr><tr><td><code>set</code></td><td><code>&#x3C;-type=value> [-parentPath=value] [-propName=value] &#x3C;jsonValue></code></td></tr><tr><td><code>tui</code></td><td></td></tr></tbody></table>

</details>

<details>

<summary>Language Studio</summary>

You can use the following commands to build your own language:

<table><thead><tr><th width="129.99481201171875">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>mklang</code></td><td><code>[-tui] &#x3C;pathtotranslations></code></td></tr></tbody></table>

</details>

<details>

<summary>Mail Shell</summary>

This shell allows you to check your e-mails and send them. You can use the following commands from Nitrocid's UESH shell:

<table><thead><tr><th width="131.328125">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>mail</code></td><td><code>[emailAddress]</code></td></tr><tr><td><code>popmail</code></td><td><code>[emailAddress]</code></td></tr><tr><td><code>ispinfo</code></td><td><code>[-host] &#x3C;emailAddressOrHost></code></td></tr></tbody></table>

You can use the following commands in the mail shell:

<table><thead><tr><th width="130.661376953125">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>cd</code></td><td><code>&#x3C;folder></code></td></tr><tr><td><code>detach</code></td><td></td></tr><tr><td><code>ispinfo</code></td><td></td></tr><tr><td><code>lsdirs</code></td><td></td></tr><tr><td><code>list</code></td><td><code>[pagenum]</code></td></tr><tr><td><code>mkdir</code></td><td><code>&#x3C;foldername></code></td></tr><tr><td><code>mv</code></td><td><code>&#x3C;mailid> &#x3C;targetfolder></code></td></tr><tr><td><code>mvall</code></td><td><code>&#x3C;sendername> &#x3C;targetfolder></code></td></tr><tr><td><code>read</code></td><td><code>&#x3C;mailid></code></td></tr><tr><td><code>readenc</code></td><td><code>&#x3C;mailid></code></td></tr><tr><td><code>ren</code></td><td><code>&#x3C;oldfoldername> &#x3C;newfoldername></code></td></tr><tr><td><code>rm</code></td><td><code>&#x3C;mailid></code></td></tr><tr><td><code>rmall</code></td><td><code>&#x3C;sendername></code></td></tr><tr><td><code>rmdir</code></td><td><code>&#x3C;foldername></code></td></tr><tr><td><code>send</code></td><td></td></tr><tr><td><code>sendenc</code></td><td></td></tr><tr><td><code>tui</code></td><td></td></tr></tbody></table>

</details>

<details>

<summary>Mod management</summary>

You can manage your mods using the following commands:

<table><thead><tr><th width="129.66668701171875">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>modmanual</code></td><td><code>&#x3C;modname></code></td></tr><tr><td><code>modman</code></td><td><p><code>&#x3C;start/stop/info/reload/install/</code></p><p><code>uninstall> &#x3C;modfilename></code></p></td></tr><tr><td></td><td><p><code>&#x3C;list/reloadall/stopall/startall/</code></p><p><code>tui></code></p></td></tr></tbody></table>

</details>

<details>

<summary>Name generator</summary>

You can generate names by using the following commands:

<table><thead><tr><th width="149.9947509765625">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>findfirstname</code></td><td><code>[-t] [term] [nameprefix] [namesuffix]</code></td></tr><tr><td><code>findsurname</code></td><td><code>[term] [surnameprefix] [surnamesuffix]</code></td></tr><tr><td><code>genname</code></td><td><code>[-t] &#x3C;namescount> [nameprefix] [namesuffix] [surnameprefix] [surnamesuffix]</code></td></tr></tbody></table>

</details>

<details>

<summary>Notes</summary>

You can jot down notes by using the following commands:

<table><thead><tr><th width="139.99481201171875">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>addnote</code></td><td><code>&#x3C;contents></code></td></tr><tr><td><code>listnotes</code></td><td></td></tr><tr><td><code>notestui</code></td><td></td></tr><tr><td><code>reloadnotes</code></td><td></td></tr><tr><td><code>removenote</code></td><td><code>&#x3C;notenum></code></td></tr><tr><td><code>removenotes</code></td><td></td></tr><tr><td><code>savenotes</code></td><td></td></tr></tbody></table>

</details>

<details>

<summary>Pastebin</summary>

This shell allows you to send either a file or a string to one of the pastebin providers. You can use the following commands:

<table><thead><tr><th width="128.99993896484375">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>pastebin</code></td><td><code>[-provider=address:host|-type=raw/http/https|-postpage=path/to/remote/post|-postformat=text/json] &#x3C;file/string></code></td></tr></tbody></table>

</details>

<details>

<summary>RSS Shell</summary>

You can use this shell to read your RSS feeds using the `rss` command. You can use the following commands from Nitrocid's UESH shell:

<table><thead><tr><th width="130.66143798828125">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>rss</code></td><td><code>[-tui] &#x3C;feedlink></code></td></tr></tbody></table>

You can use the following commands in the RSS shell:

<table><thead><tr><th width="140.661376953125">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>articleinfo</code></td><td><code>&#x3C;feednum></code></td></tr><tr><td><code>bookmark</code></td><td></td></tr><tr><td><code>detach</code></td><td></td></tr><tr><td><code>feedinfo</code></td><td></td></tr><tr><td><code>list</code></td><td></td></tr><tr><td><code>listbookmark</code></td><td></td></tr><tr><td><code>read</code></td><td><code>&#x3C;feednum></code></td></tr><tr><td><code>selfeed</code></td><td><code>&#x3C;phrase></code></td></tr><tr><td><code>search</code></td><td><code>[-t|-d|-a|-cs] &#x3C;phrase></code></td></tr><tr><td><code>unbookmark</code></td><td></td></tr></tbody></table>

</details>

<details>

<summary>SFTP Shell</summary>

SFTP shell allows you to interact with the SFTP servers. You can use the following commands from Nitrocid's UESH shell:

<table><thead><tr><th width="129.9947509765625">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>sftp</code></td><td><code>[server]</code></td></tr></tbody></table>

You can use the following commands in the SFTP shell:

<table><thead><tr><th width="129.99481201171875">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>cat</code></td><td><code>&#x3C;file></code></td></tr><tr><td><code>cdl</code></td><td><code>&#x3C;dir></code></td></tr><tr><td><code>cdr</code></td><td><code>&#x3C;dir></code></td></tr><tr><td><code>del</code></td><td><code>&#x3C;file></code></td></tr><tr><td><code>detach</code></td><td></td></tr><tr><td><code>get</code></td><td><code>&#x3C;file></code></td></tr><tr><td><code>ifm</code></td><td></td></tr><tr><td><code>lsl</code></td><td><code>[-showdetails|-suppressmessages] [dir]</code></td></tr><tr><td><code>lsr</code></td><td><code>[-showdetails] [dir]</code></td></tr><tr><td><code>mkldir</code></td><td><code>&#x3C;directory></code></td></tr><tr><td><code>mkrdir</code></td><td><code>&#x3C;directory></code></td></tr><tr><td><code>put</code></td><td><code>&#x3C;file></code></td></tr><tr><td><code>pwdl</code></td><td></td></tr><tr><td><code>pwdr</code></td><td></td></tr></tbody></table>

</details>

<details>

<summary>SQL Shell</summary>

This shell allows you to execute commands from the connected SQLite database file. You can use the below commands:

<table><thead><tr><th width="129.328125">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>cmd</code></td><td><code>&#x3C;query></code></td></tr><tr><td><code>dbinfo</code></td><td></td></tr><tr><td><code>tui</code></td><td></td></tr></tbody></table>

</details>

<details>

<summary>Stocks</summary>

This addon provides you with the following commands to query stock price info:

<table><thead><tr><th width="130.6614990234375">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>stock</code></td><td><code>[company]</code></td></tr></tbody></table>

</details>

<details>

<summary>Theme Studio</summary>

You can make your own precious and epic themes by using the following commands:

<table><thead><tr><th width="129.328125">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>mktheme</code></td><td><code>[-tui] &#x3C;themename></code></td></tr></tbody></table>

</details>

<details>

<summary>To-do List</summary>

You can build your own task list using the following commands:

<table><thead><tr><th width="129.99481201171875">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>todo</code></td><td><code>&#x3C;add> &#x3C;taskname></code></td></tr><tr><td></td><td><code>&#x3C;remove> &#x3C;taskname></code></td></tr><tr><td></td><td><code>&#x3C;done> &#x3C;taskname></code></td></tr><tr><td></td><td><code>&#x3C;undone> &#x3C;taskname></code></td></tr><tr><td></td><td><code>&#x3C;list></code></td></tr><tr><td></td><td><code>&#x3C;save></code></td></tr><tr><td></td><td><code>&#x3C;load></code></td></tr></tbody></table>

</details>

<details>

<summary>Unit conversion</summary>

You can initiate unit conversion using the following commands:

<table><thead><tr><th width="129.9947509765625">Commands</th><th>Arguments and Switches</th></tr></thead><tbody><tr><td><code>listunits</code></td><td><code>&#x3C;type></code></td></tr><tr><td><code>unitconv</code></td><td><code>[-tui] &#x3C;unittype> &#x3C;quantity> &#x3C;sourceunit> &#x3C;targetunit></code></td></tr></tbody></table>

</details>
