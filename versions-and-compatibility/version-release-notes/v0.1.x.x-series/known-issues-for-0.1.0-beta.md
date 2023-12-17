---
description: Beware! There are spike strips on the road!
---

# ⚠ Known issues for 0.1.0 Beta

There are no beta versions without any known issues discovered by either the development team of a software or the quality assurance team. Nitrocid KS is no exception.

## 0.1.0 Beta 1

During quality assurance, we're aware of the following issues:

* _FallingLines may experience visual artifacts upon fading out the lines._
* `langman reload <lang>` may fail to reload the custom language.
* Progress notifications may fail to show up properly after the normal notification.
* _`dotnet` may fail to build Nitrocid KS 0.1.0 Beta 1 in the `Release` configuration if you're building against the `v0.1.0-b1` tag._
* The kernel may fail to download debug data if the debugging symbol file is not found.

Issues that are highlighted in italic are fixed in the below beta version.

## 0.1.0 Beta 2

During quality assurance, we're aware of the following issues:

* _`langman reload <lang>` may fail to reload the custom language._
* _Progress notifications may fail to show up properly after the normal notification._
* _The kernel may fail to download debug data if the debugging symbol file is not found._
* _Letting the screen lock after timeout may cause no prompt to show._
* _Download command doesn't support downloading more than 2 GB._

Issues that are highlighted in italic are fixed in the below beta version.

## 0.1.0 Beta 3

During quality assurance, we're aware of the following issues:

* Screensaver locking on UESH may not reset the cursor state
* Archive shell may fail to start with SharpCompress not being found
  * Workaround: copy both `ZstdSharp.dll` and `SharpCompress.dll` files from RetroKS addon directory to the Archive addon directory
* Nitrocid KS currently requires administrative privileges to run
* Language studio may fail to start with this error:
  * `Command aborted for the following reason: Error reading JObject from JsonReader. Current JsonReader item is not an object: StartArray. Path '', line 1, position 1.`
* Figlet text for "Please wait" may get glitched on 80x24 terminals.
* Saving events and reminders might fail
  * Workaround: make an empty text file with the name of the event or the reminder as the error message indicates using `mkfile`.

Issues that are highlighted in italic are fixed in the upcoming release candidate version.

## Found an issue?

If you found any issue not listed above, report it using the `Report an issue` link.
