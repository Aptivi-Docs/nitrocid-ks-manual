---
description: This page describes how to make your own kernel splash using Visual Studio.
---

# 🪄 Your Splash

You're looking to create a splash for Nitrocid KS! That's great! Make sure that you have Visual Studio installed. Follow the steps to create your first splash.

1.  Press `Create a new project` on Visual Studio homepage

    <figure><img src="../../../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>
2.  Find `Class Library` and double-click it

    <figure><img src="../../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>
3.  Write your splash name, like in our example, `MyFirstSplash`.

    <figure><img src="../../../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>
4.  Make sure that `.NET 6.0` is used. Press `Create`.

    <figure><img src="../../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>
5.  Right-click on `Dependencies` -> `Manage NuGet Packages`, find `KS`, and install it.

    <figure><img src="../../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>
6.  Once the package is installed, go to the `Class1.cs` source file

    <figure><img src="../../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>
7.  In your class, implement `ISplash`, ensuring that `KS.Misc.Splash` is imported. Then, implement all the members and properties of the interface.

    <figure><img src="../../../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>
8.  Once you're done implementing all the required methods and properties, remove all references to `NotImplementedException`. It should look like below:

    <figure><img src="../../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>
9.  Once you're done, click on `Build Solution`.

    <figure><img src="../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>
10. Once the solution is built, open the file explorer to the solution directory by right-clicking on the solution and selecting `Open Folder in File Explorer`.

    <figure><img src="../../../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>
11. Navigate to the output directory and copy the `.dll` file to `KSSplashes` under the `%localappdata%/KS` folder.

    <figure><img src="../../../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>
12. Open Nitrocid KS to go to `Settings` > `General` > `Splash name`. Ensure that your splash shows up.

    <figure><img src="../../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>
