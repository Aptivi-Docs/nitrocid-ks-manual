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

* `langman reload <lang>` may fail to reload the custom language.
* _Progress notifications may fail to show up properly after the normal notification._
* The kernel may fail to download debug data if the debugging symbol file is not found.
* _Letting the screen lock after timeout may cause no prompt to show._
* Download command doesn't support downloading more than 2 GB.

Issues that are highlighted in italic are fixed in the upcoming beta version.

## Found an issue?

If you found any issue not listed above, report it using the `Report an issue` link.
