---
description: Let's keep the journals here.
---

# 📒 Kernel Journaling

Kernel journals are JSON files that tell you how the kernel is going, such as the boot process and raised events. They are serialized to the journal entry class, `JournalEntry`, which you can get all of the current session's kernel journals by using a function, `GetJournalEntries()`. Each entry contains the following items:

* `Date`: the date in which the event happened.
* `Time`: the time in which the event happened.
* `Status`: The status of the journal that can be expressed by the JournalStatus instances.
* `Message`: The contents of the journal.

Each kernel session contains a JSON file that has the following format:

```json
[
  {
    "date": "Friday, September 8, 2023",
    "time": "9:29:05 AM",
    "status": "Info",
    "message": "Kernel event fired: FileCreated [2]"
  },
  (...)
]
```

This JSON file is serialized as an array of `JournalEntry` instances.
