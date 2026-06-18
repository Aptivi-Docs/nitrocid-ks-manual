---
description: Build the simulator on macOS!
icon: apple
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/building-the-kernel/building-on-macos
---

# Building on macOS

In macOS systems, you can comfortably build Nitrocid using the command line, since it's the most lightweight solution. However, you must have the prerequisites before being able to build Nitrocid.

* [.NET 10.0 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/10.0)
* [Git for macOS](https://git-scm.com/download/mac)

***

## <mark style="color:$primary;">Using the command-line</mark>

If you are a hardcore command-line user or if you prefer using the command-line, follow these steps to build Nitrocid right from the command line:

{% stepper %}
{% step %}
#### <mark style="color:$primary;">Open your terminal emulator</mark>

Open your terminal emulator (preferrably iTerm2) on your work directory
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Clone the repository</mark>

Execute `git clone https://github.com/Aptivi/Nitrocid.git`
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Build the repository</mark>

Navigate to the cloned repository, `Nitrocid`, then execute `dotnet restore` and `dotnet build`
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Run the project</mark>

After building is done, run `dotnet run`
{% endstep %}
{% endstepper %}
