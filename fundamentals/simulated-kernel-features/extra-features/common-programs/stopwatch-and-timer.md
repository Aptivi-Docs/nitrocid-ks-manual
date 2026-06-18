---
description: >-
  Stopwatch for your favorite races, Pomodoro for task management, and timer to
  time yourself in some process
icon: alarm-clock
---

# Timers

{% hint style="info" %}
Nitrocid KS provides this feature as an addon.
{% endhint %}

The stopwatch is a timepiece that measures the elapsed time between the activation time and the current time. Generally, they're used to measure how much time did doing a specific thing take. The most famous example of a stopwatch is the stop clock, which is used in sports to measure the time between the start of the game and the current time.

Additionally, some stopwatches provide the laps system, which is useful for sports game that contains the laps, like racing or running.

The timer, however, counts down from the set time, usually minutes, to zero to set the target time. Once the time is up, the timer rings. It's used to limit the time in any action that should be done by humans.

The pomodoro timer allows you to set a 20 to 50-minute work job for a long work, set short breaks until you complete the four pomodori, then take a long break (20 to 30-minute break). This is effective in letting you work more efficiently.

The simulated kernel attempts to simulate the three features, which can be invoked by the two commands that will be listed below.

### Timer

<figure><img src="../../../../.gitbook/assets/036-timer.png" alt=""><figcaption></figcaption></figure>

The simulated kernel powers the timer feature that, by default, sets the remaining time to just one minute. The controls are:

* `ENTER`: Start counting down from the set time or reset counting down
* `T`: Specifies the remaining time
* `ESC`: Exits the application

You can start the application up with the `timer` command.

### Stopwatch

<figure><img src="../../../../.gitbook/assets/037-stopwatch.png" alt=""><figcaption></figcaption></figure>

The simulated kernel also simulates the stopwatch functionality with the ability to set the laps. You can also reset the stopwatch. The controls are:

* `ENTER`: Starts counting up the time or stops the entire stopwatch
* `L`: Sets the lap on the current elapsed time
* `SHIFT + L`: Shows a complete list of laps in an informational box
* `R`: Resets the stopwatch and its laps
* `ESC`: Exits the application

You can start the application up with the `stopwatch` command.

## Pomodoro

<figure><img src="../../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

The Pomodoro timer is provided to you by the kernel addon to simplify the task of dividing time into break segments. The controls are:

* `ENTER`: Start counting down from the set time or reset counting down
* `T`: Specifies the work time
* `B`: Specifies the break time
* `ESC`: Exits the application

You can start the application up with the `pomodoro` command.
