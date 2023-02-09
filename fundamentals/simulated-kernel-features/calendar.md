---
description: Calendars, events, and reminders
---

# 🗓 Calendar

The calendar shows you days, weeks, and months within the selected year. It not only shows how many days in a month, but it also shows the weekends in a special color or formatting and the business days in the normal color. A calendar can handle events in either a single day or within a day range. Modern calendars get synced with the latest holidays in your country.

The simulated kernel provides you with the calendar management application that attempts to simulate the above functionality. Choose a function to get started. In summary, these usages are found within the `calendar` command.

* `calendar <show> [year] [month]`
* `calendar <event> <add> <date> <title>`
* `calendar <event> <remove> <eventid>`
* `calendar <event> <list>`
* `calendar <event> <saveall>`
* `calendar <reminder> <add> <dateandtime> <title>`
* `calendar <reminder> <remove> <reminderid>`
* `calendar <reminder> <list>`
* `calendar <reminder> <saveall>`

### Showing the Calendar

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

The calendar can be shown to show you either the current month or the selected year in the current month or the selected year and month. To utilize the functionality, use the following command.

* `calendar <show>`
  * Shows you the calendar in the current year and month
* `calendar <show> [year]`
  * Shows you the calendar in the selected year in the current month
* `calendar <show> [year] [month]`
  * Shows you the calendar in the selected year and month

### Events

<figure><img src="../../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

If there is a particular event that will happen in the future, you can use this subcommand to manage your events.

* `calendar <event> <add> <date> <title>`
  * This command lets you add the event to the specified date with the title
* `calendar <event> <remove> <eventid>`
  * This command lets you remove the event by ID. You can use the below command to list all the events and their IDs.
* `calendar <event> <list>`
  * This command lets you list all the events and their IDs
* `calendar <event> <saveall>`
  * This command lets you save all the events to your kernel configuration directory. The events will get loaded upon startup.

### Reminders

<figure><img src="../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

If you would like to be reminded about something in the future, you can use this subcommand to manage your reminders.

* `calendar <reminder> <add> <dateandtime> <title>`
  * This command lets you add the reminder to the specified date and time with the title
* `calendar <reminder> <remove> <reminderid>`
  * This command lets you remove the reminder by ID. You can use the below command to list all the reminders and their IDs.
* `calendar <reminder> <list>`
  * This command lets you list all the reminders and their IDs
* `calendar <reminder> <saveall>`
  * This command lets you save all the reminders to your kernel configuration directory. The reminders will get loaded upon startup.
