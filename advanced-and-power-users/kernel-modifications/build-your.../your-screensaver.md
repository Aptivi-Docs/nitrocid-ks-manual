---
description: >-
  This page describes how to make your own custom screensaver using Visual
  Studio.
---

# 🌌 Your Screensaver

You're looking to create a screensaver for Nitrocid KS! That's great! Make sure that you have Visual Studio installed. Follow the steps to create your first screensaver.

1.  Press `Create a new project` on Visual Studio homepage

    <figure><img src="../../../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>
2.  Find `Class Library` and double-click it

    <figure><img src="../../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>
3.  Write your screensaver name, like in our example, `MyFirstScreensaver`.

    <figure><img src="../../../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>
4.  Make sure that `.NET 6.0` is used. Press `Create`.

    <figure><img src="../../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>
5.  Right-click on `Dependencies` -> `Manage NuGet Packages`, find `KS`, and install it.

    <figure><img src="../../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>
6.  Once the package is installed, go to the `Class1.cs` source file

    <figure><img src="../../../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>
7.  In your class, implement both `BaseScreensaver` and `IScreensaver`, ensuring that `KS.Misc.Screensaver` is imported.

    <figure><img src="../../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>
8.  Override the methods and properties that start with Screensaver (`ScreensaverPreparation()` and `ScreensaverOutro()` are optional), just like below:

    <figure><img src="../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>
9.  Once you have all the required methods and properties overridden like below, you can start working on your state-of-the-art screensaver using the available console tools.

    <figure><img src="../../../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>
10. Once you're done, click on `Build Solution`.

    <figure><img src="../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>
11. Once the solution is built, open the file explorer to the solution directory by right-clicking on the solution and selecting `Open Folder in File Explorer`.

    <figure><img src="../../../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>
12. Navigate to the output directory and copy the `.dll` file to `KSMods` under the `%localappdata%/KS` folder.

    <figure><img src="../../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>
13. Open Nitrocid KS to test your mod. Ensure that `savescreen YourSaver` shows your own screensaver.

    <figure><img src="../../../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

