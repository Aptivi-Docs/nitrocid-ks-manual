---
description: This page describes how to make your own kernel splash using Visual Studio.
---

# 🪄 Your Splash

You're looking to create a splash for Nitrocid KS! That's great! Make sure that you have Visual Studio installed. Follow the steps to create your first splash.

1.  Press `Create a new project` on Visual Studio homepage

    <figure><img src="../../../.gitbook/assets/Beta3-067-Adv-Building-Mod-VS.png" alt=""><figcaption></figcaption></figure>
2.  Find `Class Library` and double-click it

    <figure><img src="../../../.gitbook/assets/Beta3-068-Adv-Building-Mod-VS.png" alt=""><figcaption></figcaption></figure>
3.  Write your splash name, like in our example, `NitrocidSplash`.

    <figure><img src="../../../.gitbook/assets/Beta3-080-Adv-Building-Splash-VS.png" alt=""><figcaption></figcaption></figure>
4.  Make sure that `.NET 8.0` is used. Press `Create`.

    <figure><img src="../../../.gitbook/assets/Beta3-070-Adv-Building-Mod-VS.png" alt=""><figcaption></figcaption></figure>
5.  Right-click on `Dependencies` -> `Manage NuGet Packages`, find `KS`, and install it.

    <figure><img src="../../../.gitbook/assets/Beta3-081-Adv-Building-Splash-VS.png" alt=""><figcaption></figcaption></figure>
6.  Once the package is installed, go to the `Class1.cs` source file

    <figure><img src="../../../.gitbook/assets/Beta3-082-Adv-Building-Splash-VS.png" alt=""><figcaption></figcaption></figure>
7.  In your class, implement `ISplash` and `BaseSplash`, ensuring that `KS.Misc.Splash` is imported. Then, implement all the members and properties of the interface.

    <figure><img src="../../../.gitbook/assets/Beta3-083-Adv-Building-Splash-VS.png" alt=""><figcaption></figcaption></figure>
8.  Once you're done implementing all the required methods and properties, remove all references to `NotImplementedException`. It should look like below:

    <figure><img src="../../../.gitbook/assets/Beta3-084-Adv-Building-Splash-VS.png" alt=""><figcaption></figcaption></figure>
9.  Once you're done, follow the steps on how to create a strong name signing key and [sign your splash](https://learn.microsoft.com/en-us/dotnet/standard/assembly/sign-strong-name). Then, click on `Build Solution`.

    <figure><img src="../../../.gitbook/assets/Beta3-085-Adv-Building-Splash-VS.png" alt=""><figcaption></figcaption></figure>
10. Once the solution is built, open the file explorer to the solution directory by right-clicking on the solution and selecting `Open Folder in File Explorer`.

    <figure><img src="../../../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>
11. Navigate to the output directory and copy the `.dll` file to `KSSplashes` under the `%localappdata%/KS` folder.

    <figure><img src="../../../.gitbook/assets/Beta3-086-Adv-Building-Splash-VS.png" alt=""><figcaption></figcaption></figure>
12. Open Nitrocid KS to go to `Settings` > `General` > `Splash name`. Ensure that your splash shows up.

    <figure><img src="../../../.gitbook/assets/Beta3-087-Adv-Building-Splash-VS.png" alt=""><figcaption></figcaption></figure>
