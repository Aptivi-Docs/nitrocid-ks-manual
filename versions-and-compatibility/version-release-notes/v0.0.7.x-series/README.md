---
description: Did you plug the device in?
icon: plug
---

# v0.0.7.x series

<figure><img src="https://officialaptivi.files.wordpress.com/2022/02/68747470733a2f2f692e696d6775722e636f6d2f776870656135482e706e67.png" alt=""><figcaption></figcaption></figure>

This series marks the moment when the documentation moved to GitHub Wiki, which was an advancement for the documentation. However, this release wasn't as big as all the major first-gen releases.

Out of all the version series that provided minor updates, this series is the only one that its first digit in the last version section denotes the feature pack and its second digit informs you about how many patches applied. This was because semantic versioning limits the version parts to four parts.

For beta versions of this series, consult the below link.

{% content-ref url="v0.0.7.0-beta-versions.md" %}
[v0.0.7.0-beta-versions.md](v0.0.7.0-beta-versions.md)
{% endcontent-ref %}

***

## <mark style="color:$primary;">Versions</mark>

Here are the versions that were released:

<details>

<summary>Version 0.0.7.0</summary>

This version was released on August 30, 2019 to remove the manual page viewer from the kernel and add FTPS.

#### <mark style="color:$primary;">Additions</mark>

* <mark style="color:green;">Added FTPS</mark>

#### <mark style="color:$primary;">Improvements</mark>

* <mark style="color:yellow;">Fixed listing directories that have spaces in them</mark>
* <mark style="color:yellow;">General improvements</mark>

#### <mark style="color:$primary;">Removals</mark>

* <mark style="color:red;">Removed network pinging</mark>
* <mark style="color:red;">Removed listing computers</mark>
* <mark style="color:red;">Removed manual page viewer</mark>

</details>

<details>

<summary>Version 0.0.7.1</summary>

This version was named to be the first feature pack for the series, which was released on August 31, 2019.

#### <mark style="color:$primary;">Additions</mark>

* <mark style="color:green;">Added the Indonesian, Polish, Romanian, and Uzbekistan languages</mark>
* <mark style="color:green;">Added remote debugging</mark>
* <mark style="color:green;">Added the get command to download URLs</mark>

#### <mark style="color:$primary;">Improvements</mark>

* <mark style="color:yellow;">Configuration improvements regarding colors</mark>
* <mark style="color:yellow;">Updated the FTP library, FluentFTP</mark>

#### <mark style="color:$primary;">Removals</mark>

* <mark style="color:red;">Removed the useddeps command</mark>

</details>

<details>

<summary>Version 0.0.7.11</summary>

This version, which was released on September 3, 2019, was the first patch for the first feature pack.

#### <mark style="color:$primary;">Improvements</mark>

* <mark style="color:yellow;">Argument injector checks for arguments</mark>
* <mark style="color:yellow;">showtdzone can now show time in a specific time zone</mark>
* <mark style="color:yellow;">Added several error handlers to several commands, including chdir and chpwd</mark>
* <mark style="color:yellow;">netinfo looks tidier</mark>
* <mark style="color:yellow;">Various fixes</mark>

</details>

<details>

<summary>Version 0.0.7.12</summary>

This version was out on September 5, 2019.

#### <mark style="color:$primary;">Additions</mark>

* <mark style="color:green;">Customizability of the remote debug port and download retry count</mark>

#### <mark style="color:$primary;">Improvements</mark>

* <mark style="color:yellow;">Fixed get not downloading anything containing the URL query strings</mark>

</details>

<details>

<summary>Version 0.0.7.13</summary>

This was released on September 15, 2019, to add the built-in chat feature for remote debugger.

#### <mark style="color:$primary;">Additions</mark>

* <mark style="color:green;">Added the built-in chat on remote debugger console</mark>

#### <mark style="color:$primary;">Improvements</mark>

* <mark style="color:yellow;">Fixed invalid arguments returning wrong exception</mark>
* <mark style="color:yellow;">Improved the quiet kernel system</mark>

</details>

<details>

<summary>Version 0.0.7.14</summary>

This version was out on September 21, 2019.

#### <mark style="color:$primary;">Improvements</mark>

* <mark style="color:yellow;">Fixed defect in the remote debug chat system causing chats to take turns</mark>

</details>

<details>

<summary>Version 0.0.7.2</summary>

This version was named as the second feature release for this series, and it was released on September 23, 2019.

#### <mark style="color:$primary;">Additions</mark>

* <mark style="color:green;">Added Yellow background (YellowBG) and foreground (YellowFG) themes</mark>
* <mark style="color:green;">Added the Japanese language</mark>

#### <mark style="color:$primary;">Improvements</mark>

* <mark style="color:yellow;">Updated the FTP library, FluentFTP</mark>
* <mark style="color:yellow;">Time zone offsets are now shown</mark>
* <mark style="color:yellow;">Fixed several graphics artifacts regarding light backgrounds and time/date corner widget</mark>

</details>

<details>

<summary>Version 0.0.7.21</summary>

This version was out on September 29, 2019 to make improvements.

#### <mark style="color:$primary;">Improvements</mark>

* <mark style="color:yellow;">Fixed Japanese language not keeping up with the latest strings</mark>
* <mark style="color:yellow;">Fixed FTP connection routine not prompting the user for profile selection</mark>
* <mark style="color:yellow;">General improvements</mark>

</details>

<details>

<summary>Version 0.0.7.3</summary>

This version was released on October 4, 2019 to bring the third feature package to the series.

#### <mark style="color:$primary;">Additions</mark>

* <mark style="color:green;">Added command support to remote debugger</mark>
* <mark style="color:green;">Added Arabic transliteration</mark>

#### <mark style="color:$primary;">Improvements</mark>

* <mark style="color:yellow;">Fixed empty address being accepted in the connect FTP command</mark>
* <mark style="color:yellow;">Fixed crash when trying to handle non-socket problems</mark>

</details>

<details>

<summary>Version 0.0.7.4</summary>

This version started the fourth feature package for this series, which appeared on October 18, 2019.

#### <mark style="color:$primary;">Additions</mark>

* <mark style="color:green;">Added kernel test shell</mark>
* <mark style="color:green;">Added debug quota</mark>

#### <mark style="color:$primary;">Improvements</mark>

* <mark style="color:yellow;">Fixed debugger not flushing info to the debug file after clearing debug log</mark>
* <mark style="color:yellow;">Updated the FTP library, FluentFTP</mark>
* <mark style="color:yellow;">Improved NuGet packaging</mark>

</details>

<details>

<summary>Version 0.0.7.41</summary>

On October 19, 2019, this patch got released.

#### <mark style="color:$primary;">Improvements</mark>

* <mark style="color:yellow;">Fixed progress bar causing color bleed (using default console color)</mark>
* <mark style="color:yellow;">Clarified the ETA for FTP file transfer</mark>

</details>

<details>

<summary>Version 0.0.7.5</summary>

This is the fifth feature update to the 0.0.7.x series that got released on October 24, 2019.

#### <mark style="color:$primary;">Additions</mark>

* <mark style="color:green;">Argument support to the remote debug commands is now added</mark>
* <mark style="color:green;">Added the username debug command</mark>
* <mark style="color:green;">Added the stack trace viewer trace</mark>

#### <mark style="color:$primary;">Improvements</mark>

* <mark style="color:yellow;">Two newly-added shells now complain when the specified command wasn't found</mark>
* <mark style="color:yellow;">Fixed stack trace history not getting updated in some cases</mark>

</details>

<details>

<summary>Version 0.0.7.6</summary>

This version was out on October 29, 2019 as a last feature update for this series.

#### <mark style="color:$primary;">Additions</mark>

* <mark style="color:green;">Added naming system to the remote debugger chat (generated names only)</mark>
* <mark style="color:green;">Added the lines and glitterMatrix screensavers</mark>

#### <mark style="color:$primary;">Improvements</mark>

* <mark style="color:yellow;">Extended debugging to more areas of the kernel</mark>

</details>

<details>

<summary>Version 0.0.7.61</summary>

This was the last version of the kernel to declare itself as API v1.0. It got released on October 30, 2019 to bring several fixes.

#### <mark style="color:$primary;">Additions</mark>

* <mark style="color:green;">Added the transliterated Russian language</mark>

#### <mark style="color:$primary;">Improvements</mark>

* <mark style="color:yellow;">Fixed crash on startup in modded kernels</mark>
* <mark style="color:yellow;">Fixed translations</mark>
* <mark style="color:yellow;">Custom screensavers can now cause console cursor to disappear</mark>

</details>
