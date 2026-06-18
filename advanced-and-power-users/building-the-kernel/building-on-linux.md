---
description: Build the simulator on Linux!
icon: linux
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/building-the-kernel/building-on-linux
---

# Building on Linux

In Linux systems, you can comfortably build Nitrocid using the command line, since it's the most lightweight solution. However, you must have the prerequisites before being able to build Nitrocid.

* [.NET 10.0 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/10.0)

***

## <mark style="color:$primary;">Using the command-line</mark>

If you are a hardcore command-line user or if you prefer using the command-line, follow these steps to build Nitrocid right from the command line:

{% stepper %}
{% step %}
#### <mark style="color:$primary;">Open your terminal emulator</mark>

Open your terminal emulator on your work directory
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Clone the repository</mark>

Execute `git clone https://github.com/Aptivi/Nitrocid.git`
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Build the repository</mark>

Navigate to the cloned repository, `Nitrocid`, then execute `make dbg` for debug builds and `make` for release builds, or `dotnet restore` and `dotnet build`
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Run the project</mark>

After building is done, run `dotnet run`
{% endstep %}
{% endstepper %}

{% hint style="info" %}
We recommend that you use `make` to build Nitrocid, since it automatically checks for .NET installation and prepares the environment
{% endhint %}
