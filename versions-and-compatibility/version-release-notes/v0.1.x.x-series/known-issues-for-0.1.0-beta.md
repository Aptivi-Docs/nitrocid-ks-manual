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

* _Screensaver locking on UESH may not reset the cursor state_
* _Archive shell may fail to start with SharpCompress not being found_
  * _Workaround: copy both `ZstdSharp.dll` and `SharpCompress.dll` files from RetroKS addon directory to the Archive addon directory_
* _Nitrocid KS currently requires administrative privileges to run_
* _Language studio may fail to start with this error:_
  * _`Command aborted for the following reason: Error reading JObject from JsonReader. Current JsonReader item is not an object: StartArray. Path '', line 1, position 1.`_
* _Figlet text for "Please wait" may get glitched on 80x24 terminals._
* _Saving events and reminders might fail_
  * _Workaround: make an empty text file with the name of the event or the reminder as the error message indicates using `mkfile`._

Issues that are highlighted in italic are fixed in the upcoming release candidate version.

## 0.1.0 Release Candidate

During quality assurance, we're aware of the following issues:

* TBD

Issues that are highlighted in italic are fixed in the final version.

## Found an issue?

If you found any issue not listed above, report it using the `Report an issue` link.
