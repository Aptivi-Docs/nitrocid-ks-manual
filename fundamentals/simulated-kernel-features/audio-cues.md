---
description: Make your kernel more groovy!
icon: volume
---

# Audio Cues

<figure><img src="../../.gitbook/assets/image (184).png" alt=""><figcaption></figcaption></figure>

Audio cues allow your kernel to make different sounds for different events, including the startup and the shutdown sound. This feature uses the BassBoom library to play such short sound files embedded inside the main Nitrocid assembly in multiple platforms. The group of short sounds or audio cues is called the audio cue container, which Nitrocid internally uses to store a group of properties that regenerate stream instances from the resource manager, due to how BassBoom's [Play-n-Forget](https://app.gitbook.com/s/VEwnv6SUh5piF7crh1UN/power-users/using-basolia/playback#playn-forget) feature works.

Every audio cue container represents a sound theme, which is managed by the audio cue tools class, `AudioCueTools`. This class is found in the `Nitrocid.Misc.Audio` namespace. The following themes can be chosen:

* `the_mirage`: The Mirage (default)
* `big_loss`: Big Loss
* `great_moments`: Great Moments
* `thousands_nights`: 00's Nights
* `the_night`: The Night

In the kernel configuration, you can turn off a specific audio cue or the entire audio cue system in the `Audio settings` category.

{% hint style="info" %}
Turning the audio cue system off turns off all the audio cue settings, and you'll have to turn them on manually the next time you want to turn the audio cues on.
{% endhint %}

## Audio cues on mods

Your mods can utilize the audio cue tools to play such short sounds that you choose according to the following types defined in the `AudioCueType` enumeration:

* `Alarm`: Intense version of the alarm sound
* `AlarmIdle`: Idle version of the alarm sound
* `Ambience`: Intense version of the ambience sound
* `AmbienceIdle`: Idle version of the ambience sound
* `BeepHigh`: High-priority beep sound
* `BeepMedium`: Medium-priority beep sound
* `BeepLow`: Low-priority beep sound
* `KeyboardCueBackspace`: Backspace keypress
* `KeyboardCueEnter`: Enter keypress
* `KeyboardCueType`: Pressing any key
* `NotificationHigh`: High-priority notifications
* `NotificationMedium`: Medium-priority notifications
* `NotificationLow`: Low-priority notifications
* `Shutdown`: Shutdown sound
* `SpecialBeep`: Special beep for special notifications
* `Startup`: Startup sound

To play audio cues, you can use one of the following functions:

{% code title="AudioCueTools.cs" lineNumbers="true" %}
```csharp
public static void PlayAudioCue(AudioCueType cueType)
public static void PlayAudioCue(AudioCueType cueType, string cueName)
public static void PlayAudioCue(AudioCueType cueType, AudioCueContainer cueContainer)
```
{% endcode %}

The first function takes an audio cue type specified above with the default audio cue. However, the last two functions specify what cue container or theme do you want by name and by the audio cue container object. However, such names are case-sensitive.

{% hint style="info" %}
You can get a list of audio cue theme names using the `GetAudioThemeNames()` function, and you can get the audio cue container instance from either the default cue theme or the specified cue theme name using the `GetAudioCue()` function.
{% endhint %}
