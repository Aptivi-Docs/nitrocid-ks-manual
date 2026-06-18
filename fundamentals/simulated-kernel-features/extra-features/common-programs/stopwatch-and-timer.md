---
description: >-
  Stopwatch for your favorite races, Pomodoro for task management, and timer to
  time yourself in some process
icon: alarm-clock
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/fundamentals/simulated-kernel-features/extra-features/common-programs/stopwatch-and-timer
---

# Timers

The stopwatch is a timepiece that measures the elapsed time between the activation time and the current time. Generally, they're used to measure how much time did doing a specific thing take.

To get started, expand a section below.

<details>

<summary>Timer</summary>

<figure><img src="../../../../.gitbook/assets/image (14) (1).png" alt=""><figcaption></figcaption></figure>

The timer counts down from the set time, usually minutes, to zero to set the target time. Once the time is up, the timer rings. It's used to limit the time in any action that should be done by humans.

The simulated kernel powers the timer feature that, by default, sets the remaining time to just one minute.

#### <mark style="color:$primary;">Usage</mark>

The controls are:

| Keybinding | Description                                                  |
| ---------- | ------------------------------------------------------------ |
| `ENTER`    | Start counting down from the set time or reset counting down |
| `T`        | Specifies the remaining time                                 |
| `ESC`      | Exits the application                                        |

{% hint style="info" %}
You can start the application up with the `timer` command.
{% endhint %}

</details>

<details>

<summary>Stopwatch</summary>

<figure><img src="../../../../.gitbook/assets/image (15) (1).png" alt=""><figcaption></figcaption></figure>

The most famous example of a stopwatch is the stop clock, which is used in sports to measure the time between the start of the game and the current time. Additionally, some stopwatches provide the laps system, which is useful for sports game that contains the laps, like racing or running.

The simulated kernel also simulates the stopwatch functionality with the ability to set the laps. You can also reset the stopwatch.

#### Usage

The controls are:

<table><thead><tr><th width="130.33331298828125">Keybinding</th><th>Description</th></tr></thead><tbody><tr><td><code>ENTER</code></td><td>Starts counting up the time or stops the entire stopwatch</td></tr><tr><td><code>L</code></td><td>Sets the lap on the current elapsed time</td></tr><tr><td><code>SHIFT + L</code></td><td>Shows a complete list of laps in an informational box</td></tr><tr><td><code>R</code></td><td>Resets the stopwatch and its laps</td></tr><tr><td><code>ESC</code></td><td>Exits the application</td></tr></tbody></table>

{% hint style="info" %}
You can start the application up with the `stopwatch` command.
{% endhint %}

</details>

<details>

<summary>Pomodoro</summary>

<figure><img src="../../../../.gitbook/assets/image (16) (1).png" alt=""><figcaption></figcaption></figure>

The pomodoro timer allows you to set a 20 to 50-minute work job for a long work, set short breaks until you complete the four pomodori, then take a long break (20 to 30-minute break). This is effective in letting you work more efficiently.

The Pomodoro timer is provided to you by the kernel addon to simplify the task of dividing time into break segments.

#### <mark style="color:$primary;">Usage</mark>

The controls are:

<table><thead><tr><th width="131.333251953125">Keybinding</th><th>Description</th></tr></thead><tbody><tr><td><code>ENTER</code></td><td>Start counting down from the set time or reset counting down</td></tr><tr><td><code>T</code></td><td>Specifies the work time</td></tr><tr><td><code>B</code></td><td>Specifies the break time</td></tr><tr><td><code>ESC</code></td><td>Exits the application</td></tr></tbody></table>

{% hint style="info" %}
You can start the application up with the `pomodoro` command.
{% endhint %}

</details>
