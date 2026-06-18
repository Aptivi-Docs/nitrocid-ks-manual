---
description: Build the simulator on macOS!
icon: freebsd
---

# Building on FreeBSD

In FreeBSD systems, you can comfortably build Nitrocid using the command line, since it's the most lightweight solution. However, you must have the prerequisites before being able to build Nitrocid.

* [.NET 10.0 SDK](https://github.com/sec/dotnet-core-freebsd-source-build/releases)
* Git for FreeBSD

***

## <mark style="color:$primary;">Using the command-line</mark>

If you are a hardcore command-line user or if you prefer using the command-line, follow these steps to build Nitrocid right from the command line:

{% stepper %}
{% step %}
### <mark style="color:$primary;">Open your terminal emulator</mark>

Open your terminal emulator (preferrably Konsole) on your work directory
{% endstep %}

{% step %}
### <mark style="color:$primary;">Clone the repository</mark>

Execute `git clone https://github.com/Aptivi/Nitrocid.git`
{% endstep %}

{% step %}
### <mark style="color:$primary;">Build the repository</mark>

Navigate to the cloned repository, `Nitrocid`, then execute `dotnet restore` and `dotnet build`&#x20;
{% endstep %}

{% step %}
### <mark style="color:$primary;">Run the project</mark>

After building is done, run `dotnet run`
{% endstep %}
{% endstepper %}
