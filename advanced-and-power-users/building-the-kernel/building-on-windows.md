---
description: Build the simulator on Windows!
icon: windows
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/building-the-kernel/building-on-windows
---

# Building on Windows

In Windows systems, you have two ways to build the simulator: one if you use Visual Studio 2026 or later, and one if you prefer doing everything via the command-line. Make sure that your computer has the following dependencies:

* [Git for Windows](https://git-scm.com/download/win)
* [.NET 10.0 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/10.0) (usually installed with Visual Studio 18.0 or later)

Choose a preferred method.

***

## <mark style="color:$primary;">Visual Studio 2026 v18.0+</mark>

Before being able to build Nitrocid, please make sure that you have at least Visual Studio 2026 version 18.0 or later that supports building projects for .NET 10.0. You can get Visual Studio [here](https://visualstudio.microsoft.com/).

Once you have Visual Studio installed with at least the .NET 10.0 SDK and the .NET development workload, follow these steps:

{% stepper %}
{% step %}
#### <mark style="color:$primary;">Open Visual Studio</mark>

Open Visual Studio and press `Clone Repository`
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Write the repository location</mark>

In the repository location field, write `https://github.com/Aptivi/Nitrocid.git`

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Clone the repository</mark>

Press `Clone`. The clone may need to take a few minutes depending on your Internet connection.
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Open Nitrocid's solution</mark>

Press `Solution Explorer` » `Switch Views` and double click on `Nitrocid.slnx`

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Build the solution</mark>

Press `F6` on your keyboard, or press `Build` » `Build Solution` to build

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Execute Nitrocid</mark>

Navigate to the build output folder, `KSBuild`, and double click on the `Nitrocid.exe` file

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>
{% endstep %}
{% endstepper %}

***

## <mark style="color:$primary;">Using the command-line</mark>

If you are a hardcore command-line user or if you prefer using the command-line, follow these steps to build Nitrocid right from the command line:

{% stepper %}
{% step %}
#### <mark style="color:$primary;">Open Git Bash</mark>

Open `Git Bash` on your work directory
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
