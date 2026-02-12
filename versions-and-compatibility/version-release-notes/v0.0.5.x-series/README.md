---
description: The time has come!
icon: clock
---

# v0.0.5.x series

The time has come to bring the series to the stable release. It added aliases, permanent color setting, and so on.

For beta versions of this series, consult the below link.

{% content-ref url="v0.0.5.0-beta-versions.md" %}
[v0.0.5.0-beta-versions.md](v0.0.5.0-beta-versions.md)
{% endcontent-ref %}

***

## <mark style="color:$primary;">Versions</mark>

Here are the versions that were released:

<details>

<summary>Version 0.0.5.0</summary>

On September 4, 2018, this version was made to start the prompt obsoletion movement and make several improvements to the beta versions of 0.0.5.

#### <mark style="color:$primary;">Additions</mark>

* <mark style="color:green;">User-made commands in mods</mark>
* <mark style="color:green;">Added the showaliases command</mark>
* <mark style="color:green;">Permanent color setting</mark>

#### <mark style="color:$primary;">Improvements</mark>

* <mark style="color:yellow;">Made several fixes, including the alias parser</mark>
* <mark style="color:yellow;">Beep command prevents frequencies more than 2048 Hz</mark>
* <mark style="color:yellow;">Removing aliases now no longer requires a command to be provided</mark>
* <mark style="color:yellow;">General improvements</mark>

#### <mark style="color:$primary;">Removals</mark>

* <mark style="color:red;">Removed prompts</mark>
* <mark style="color:red;">Removed motd, chkn=1, preadduser and hostname arguments</mark>

</details>

<details>

<summary>Version 0.0.5.1</summary>

This release only contains improvements to debugging system regarding an area of the kernel. It got released on September 6, 2018.

#### <mark style="color:$primary;">Improvements</mark>

* <mark style="color:yellow;">Improved behavior of debugging logs</mark>
* <mark style="color:yellow;">Improved a debug message</mark>
* <mark style="color:yellow;">Made changes to startup banner</mark>

</details>

<details>

<summary>Version 0.0.5.2</summary>

It got released on September 9, 2018, to make changes to graphics card parsing.

#### <mark style="color:$primary;">Improvements</mark>

* <mark style="color:yellow;">Made graphics card parsing always on startup</mark>
* <mark style="color:yellow;">Improved config updater</mark>

#### <mark style="color:$primary;">Removals</mark>

* <mark style="color:green;">Removed the gpuprobe argument</mark>

</details>

<details>

<summary>Version 0.0.5.5</summary>

On September 22, 2018, it made a major rewrite of the kernel configuration, as well as some additions and improvements. This was the last version that was unsupported on Unix systems.

#### <mark style="color:$primary;">Additions</mark>

* <mark style="color:green;">Added the FTP client</mark>
* <mark style="color:green;">Added more text placeholders, such as shortdate, longdate, etc.</mark>

#### <mark style="color:$primary;">Improvements</mark>

* <mark style="color:yellow;">Configuration system refined</mark>
* <mark style="color:yellow;">Fixed repeating memory messages</mark>
* <mark style="color:yellow;">General improvements</mark>

</details>

<details>

<summary>Version 0.0.5.6</summary>

This was the first version that ran in all Unix systems using the Mono Runtime framework. It was out on October 12, 2018.

#### <mark style="color:$primary;">Additions</mark>

* <mark style="color:green;">Support for Linux systems</mark>

#### <mark style="color:$primary;">Improvements</mark>

* <mark style="color:yellow;">Improved hardware probers</mark>
* <mark style="color:yellow;">Username list on login</mark>
* <mark style="color:yellow;">help arginj now lists improvements</mark>
* <mark style="color:yellow;">Other improvements...</mark>

</details>

<details>

<summary>Version 0.0.5.7</summary>

On October 13, 2018, several improvements to the kernel regarding Unix support surfaced.

#### <mark style="color:$primary;">Additions</mark>

* <mark style="color:green;">Print current directory in FTP shell</mark>

#### <mark style="color:$primary;">Improvements</mark>

* <mark style="color:yellow;">Fixed crash if the executable name is something other than "Kernel Simulator.exe"</mark>
* <mark style="color:yellow;">Fixed "Quiet Probe" configuration entry being set to some strange value</mark>
* <mark style="color:yellow;">Fixed a known bug affecting Unix systems</mark>

#### <mark style="color:$primary;">Removals</mark>

* <mark style="color:red;">Version command</mark>

</details>

<details>

<summary>Version 0.0.5.8</summary>

This version was released on November 1, 2018, to make several improvements to the kernel, but withdraws some features.

This release was declared to be the last release supporting Windows XP systems with .NET Framework 4.5 installed.

#### <mark style="color:$primary;">Improvements</mark>

* <mark style="color:yellow;">Even if one of the hardware failed to parse, the kernel continues to boot</mark>
* <mark style="color:yellow;">Only administrators can access reloadconfig and alias commands</mark>

#### <mark style="color:$primary;">Removals</mark>

* <mark style="color:red;">The kernel no longer beeps when rebooting and shutting down</mark>
* <mark style="color:red;">Beep command no longer exists</mark>

</details>

***

## <mark style="color:$primary;">Known bugs</mark>

Initial documentation for these versions have mentioned the following known bugs in the "`troubleshooting`" document: _(original wording preserved for brevity - only covers pre-2021 releases)_

<table><thead><tr><th width="101">Found</th><th width="94">Fixed</th><th>Description</th></tr></thead><tbody><tr><td>0.0.5.6</td><td>0.0.5.7</td><td><ol><li>[Unix] Any error messages that is handled will crash the handler with a continuable kernel error. Investigation found that something ambiguous is going on.</li></ol></td></tr></tbody></table>
