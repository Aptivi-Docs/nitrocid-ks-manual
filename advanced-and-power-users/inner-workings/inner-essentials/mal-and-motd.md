---
description: Message of the Day before and after login
---

# ✉ MAL and MOTD

Messages of the day were used before and after logging in to your user account to give you a warm greeting, a funny quote, or a text of your choice. This gives you a subtle information about your message of the day.

Nitrocid initializes your MAL and your MOTD file when the kernel boots for the first time by saving them with the defaults. The next time the kernel finds your MAL and your MOTD files, the kernel uses them to read these messages and display them before and after logging in to your user account.

### Initialization

For initialization, the `ReadMal()` and the `ReadMotd()` functions call these functions, `InitMal()` and `InitMotd()` respectively, when their associated files aren't found.

### Setting

As for saving the current messages, you can use the `SetMal()` and the `SetMotd()` functions, providing it the message that you want to save. Once done, the kernel will read your updated MOTD and MAL messages.

### Reading

When it comes to reading, `ReadMal()` and `ReadMotd()` does everything to try to read the MAL and the MOTD messages and set them to the parsed MOTD and MAL message properties.
