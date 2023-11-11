---
description: Your notifications are on your way!
---

# 🔔 System Notifications

Nitrocid KS provides a way to show the progress from specific applications or to show the update using a feature called the notifications. The kernel handles the notifications and displays all new notifications in the upper right corner of the screen.

These notifications have the following types:

* Normal notifications: these notifications contain the title and the description to tell you what you're being notified about.
* Progress notifications: these notifications contain the title, the description, and the progress data to indicate how much work is being done.
* Indeterminate progress notifications: these notifications are basically the same as the progress notifications, except that they don't provide any progress information; they just show whether the progress succeeded or failed.

### Sending notifications

If you want to send a notification indicating that there is something new, you can make a new `Notification` instance, specifying the following properties:

* Notification title
* Notification description
* Notification priority
* Notification type

{% hint style="info" %}
To make indeterminate progress notifications, you must set the notification type to `Progress` and set the `ProgressIndeterminate` property to `true` prior to sending notifications. The below example shows you how it's done:

```csharp
var Notif = new Notification(Translate.DoTranslation("Test indeterminate notification"), Translate.DoTranslation("Description is here"), NotificationPriority.Low, NotificationType.Progress)
{
    ProgressIndeterminate = true
};
NotificationManager.NotifySend(Notif);
```
{% endhint %}

{% hint style="info" %}
Progress notifications, determinate or not, are shown asynchronously. You'll have to update the `Progress` property until it reaches to 100%, depending on the job being done.

Also, it's necessary to change the notification progress state, regardless of whether the operation succeeded or not.
{% endhint %}

After creating a new instance of Notification, you'll have to use either the `NotifySend()` function to send a single notification, or the `NotifySendRange()` function to send a barrage of notifications. This is to ensure that your notification is displayed.

### Notification dismissal

If you no longer want a notification to display in the notifications list, you'll need to run the `dismissnotif` or `dismissnotifs` command. Similarly, in your mods, you'll have to call either the `NotifDismiss()` function for a single notification, or the `NotifDismissAll()` function for all notifications.

After that, the notification should be cleared from the list of recent notifications so that you can keep up with the new updates.