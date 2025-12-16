---
description: Build the simulator on Windows!
icon: windows
---

# Building on Windows

In Windows systems, you have two ways to build the simulator: one if you use Visual Studio 2026 or later, and one if you prefer doing everything via the command-line. Make sure that your computer has the following dependencies:

* [Git for Windows](https://git-scm.com/download/win)
* [.NET 10.0 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/10.0) (usually installed with Visual Studio 18.0 or later)

### Visual Studio 2026 v18.0+

Before being able to build Nitrocid KS, please make sure that you have at least Visual Studio 2026 version 18.0 or later that supports building projects for .NET 10.0. You can get Visual Studio [here](https://visualstudio.microsoft.com/).

Once you have Visual Studio installed with at least the .NET 10.0 SDK and the .NET development workload, follow these steps:

1. Open Visual Studio and press `Clone Repository`
2.  In the repository location field, write `https://github.com/Aptivi/NitrocidKS.git`\
    <br>

    <figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>
3. Press `Clone`. The clone may need to take a few minutes depending on your Internet connection.
4. Press `Solution Explorer` » `Switch Views` and double click on `Nitrocid.sln`\
   ![](<../../.gitbook/assets/image (14).png>)
5. Press `Start` or press `Build` » `Build Solution` to build\
   ![](<../../.gitbook/assets/image (15).png>)
6.  Navigate to the build output folder, `KSBuild`, and double click on the `Nitrocid.exe` file

    <figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

### Using the command-line

If you are a hardcore command-line user or if you prefer using the command-line, follow these steps to build Nitrocid KS right from the command line:

1. Open `Git Bash` on your work directory
2. Execute `git clone https://github.com/Aptivi/NitrocidKS.git`
3. Navigate to the cloned repository, `NitrocidKS`
4. Execute `dotnet restore` and `dotnet build`
5. After building is done, run `dotnet run`.
