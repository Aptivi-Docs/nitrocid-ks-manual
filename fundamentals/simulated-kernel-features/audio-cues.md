---
description: Make your kernel more groovy!
icon: volume
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/fundamentals/simulated-kernel-features/audio-cues
---

# Audio Cues

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

Audio cues allow your kernel to make different sounds for different events, including the startup and the shutdown sound. This feature uses the BassBoom library to play such short sound files embedded inside the main Nitrocid assembly in multiple platforms.

The group of short sounds or audio cues is called the audio cue container, which Nitrocid internally uses to store a group of properties that regenerate stream instances from the resource manager, due to how BassBoom's [Play-n-Forget](https://app.gitbook.com/s/VEwnv6SUh5piF7crh1UN/power-users/using-basolia/playback#playn-forget) feature works.

***

## <mark style="color:$primary;">Sound themes</mark>

Every audio cue container represents a sound theme, which is managed by the audio cue tools class, `AudioCueTools`. This class is found in the `Nitrocid.Misc.Audio` namespace.

<details>

<summary>Available themes</summary>

The following themes can be chosen:

<table><thead><tr><th width="190">Theme</th><th>Description</th></tr></thead><tbody><tr><td><code>the_mirage</code></td><td>The Mirage (default)</td></tr><tr><td><code>the_mirage_urban</code></td><td>The Mirage (Urban)</td></tr><tr><td><code>big_loss</code></td><td>Big Loss</td></tr><tr><td><code>great_moments</code></td><td>Great Moments</td></tr><tr><td><code>thousands_nights</code></td><td>00's Nights</td></tr><tr><td><code>the_night</code></td><td>The Night</td></tr><tr><td><code>implicit_rage</code></td><td>Implicit Rage</td></tr><tr><td><code>stack_trap</code></td><td>Stack Trap</td></tr><tr><td><code>the_mirage_edm</code></td><td>The Mirage (Deep House Tech)</td></tr><tr><td><code>soothing_calm</code></td><td>Soothing Calm</td></tr><tr><td><code>the_aptitude</code></td><td>The Aptitude</td></tr><tr><td><code>crossing_limits</code></td><td>Crossing Limits</td></tr><tr><td><code>future_prism</code></td><td>Future Prism</td></tr><tr><td><code>the_mirage_indian</code></td><td>The Mirage (Indian)</td></tr><tr><td><code>the_underground</code></td><td>The Underground</td></tr></tbody></table>

</details>

***

## <mark style="color:$primary;">Audio cues</mark>

Your mods can utilize the audio cue tools to play such short sounds that you choose according to the audio cue types.

<details>

<summary>Audio cue types</summary>

The types are defined in the `AudioCueType` enumeration:

|                        |                                        |
| ---------------------- | -------------------------------------- |
| `Alarm`                | Intense version of the alarm sound     |
| `AlarmIdle`            | Idle version of the alarm sound        |
| `Ambience`             | Intense version of the ambience sound  |
| `AmbienceIdle`         | Idle version of the ambience sound     |
| `BeepHigh`             | High-priority beep sound               |
| `BeepMedium`           | Medium-priority beep sound             |
| `BeepLow`              | Low-priority beep sound                |
| `KeyboardCueBackspace` | Backspace keypress                     |
| `KeyboardCueEnter`     | Enter keypress                         |
| `KeyboardCueType`      | Pressing any key                       |
| `NotificationHigh`     | High-priority notifications            |
| `NotificationMedium`   | Medium-priority notifications          |
| `NotificationLow`      | Low-priority notifications             |
| `Shutdown`             | Shutdown sound                         |
| `SpecialBeep`          | Special beep for special notifications |
| `Startup`              | Startup sound                          |

</details>

<details>

<summary>Playing audio cues</summary>

To play audio cues, you can use one of the following functions:

{% code title="AudioCueTools.cs" lineNumbers="true" %}
```csharp
public static void PlayAudioCue(AudioCueType cueType) { }
public static void PlayAudioCue(AudioCueType cueType, string cueName) { }
public static void PlayAudioCue(AudioCueType cueType, AudioCueContainer cueContainer) { }
```
{% endcode %}

The first function takes an audio cue type specified above with the default audio cue. However, the last two functions specify what cue container or theme do you want by name and by the audio cue container object. However, such names are case-sensitive.

{% hint style="info" %}
You can get a list of audio cue theme names using the `GetAudioThemeNames()` function, and you can get the audio cue container instance from either the default cue theme or the specified cue theme name using the `GetAudioCue()` function.
{% endhint %}

</details>

<details>

<summary>Controlling audio cues</summary>

In the kernel configuration, you can turn off a specific audio cue or the entire audio cue system in the `Audio settings` category.

{% hint style="info" %}
Turning the audio cue system off turns off all the audio cue settings, and you'll have to turn them on manually the next time you want to turn the audio cues on.
{% endhint %}

</details>
