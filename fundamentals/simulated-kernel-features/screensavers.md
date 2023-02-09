---
description: Screensavers and their usage
---

# 🌌 Screensavers

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

The screensavers were touted to be a solution against screen burn-ins in cathode ray-tube (CRT) or plasma displays. They fill the screens with either the blank screen or moving image or parts across the entire screen. They also are placed as a security measure so that when screensavers exit, the user will be required to input the password to be able to use your computer again.

The first screensaver that blanked the screen after three minutes of inactivity on the original IBM PCs, `scrnsave`, was created on 1983 by John Socha. Since then, improvements were made to make modern screensavers than just blanking the screen, to the point that the screensavers earned 3D support in modern times.

The simulated kernel attempts to simulate this functionality in its complete state. You can even customize most built-in screensavers using the built-in `settings` application found in the kernel, though you have to pass the `-saver` switch to it.

### Setting the screensaver

<figure><img src="../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

To set the screensaver to your favorite screensaver, use the `setsaver` command. Since this command is an administrative command, you either need to use an administrator account or use an account that has been granted the administrative command permissions.

1. Log-in to the system account, root, or any of the administrators or users that has at least the strict command running permissions
2. Execute the `setsaver` command to set the default kernel screensaver
   * The full usage of the `setsaver` command is `setsaver <(CustomSaverName)/saver>`
3. Lock or save your screen using `savescreen` or `lockscreen`.

{% hint style="info" %}
Note that your account must have either the administrative permissions enabled or the strict command running permission granted to be able to use this command.
{% endhint %}

### Saving your screen

To save your screen using your default screensaver or any other screensaver, you need to use the `savescreen` command to launch the screensaver.

### Locking your screen

To lock your screen in the simulated kernel, you need to use the `lockscreen` command to launch the screensaver. Once you press any key, you need to enter your user password before you're able to access the shell again.

### Reloading your custom screensaver

To reload your custom screensaver, just pass in your custom screensaver name to the `reloadsaver` command. This is useful in upgrades to the new version of the screensaver to make minor patches to it. Since this command is an administrative command, you either need to use an administrator account or use an account that has been granted the administrative command permissions.

1. Log-in to the system account, root, or any of the administrators or users that has at least the strict command running permissions
2. Execute the `reloadsaver` command to set the default kernel screensaver
   * The full usage of the `reloadsaver` command is `reloadsaver <CustomSaver>`
3. Save your screen using `savescreen [CustomSaver]`.

{% hint style="info" %}
Note that your account must have either the administrative permissions enabled or the strict command running permission granted to be able to use this command.
{% endhint %}
