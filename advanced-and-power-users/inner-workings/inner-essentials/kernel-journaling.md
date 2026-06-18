---
description: Let's keep the journals here.
icon: notebook
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/inner-workings/inner-essentials/kernel-journaling
---

# Kernel Journaling

<figure><img src="../../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

Kernel journals are JSON files that tell you how the kernel is going, such as the boot process and raised events. They are serialized to the journal entry class, `JournalEntry`, which you can get all of the current session's kernel journals by using a function, `GetJournalEntries()`.

<details>

<summary>Items of a journal entry</summary>

Each entry contains the following items:

<table><thead><tr><th width="99.6666259765625">Item</th><th>Description</th></tr></thead><tbody><tr><td><code>Date</code></td><td>The date in which the event happened.</td></tr><tr><td><code>Time</code></td><td>The time in which the event happened.</td></tr><tr><td><code>Status</code></td><td>The status of the journal that can be expressed by the <code>JournalStatus</code> instances.</td></tr><tr><td><code>Message</code></td><td>The contents of the journal.</td></tr></tbody></table>

</details>

<details>

<summary>JSON structure</summary>

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

This JSON file is serialized as an array of `JournalEntry` instances and is automatically saved when a write occurs.

</details>

***

## <mark style="color:$primary;">Manipulating with the Journals</mark>

You can manipulate with the kernel journals using the following available functions:

<details>

<summary>Writing to the Journal</summary>

Writing to the kernel journal is straightforward, as there are two functions that are simple to use:

```csharp
public static void WriteJournal(string Message, params object[] Vars) { }
public static void WriteJournal(string Message, JournalStatus Status, params object[] Vars) { }
```

You can write any message, like a progress of some operation, to the kernel journal using just the message as an argument. However, this message will get saved as an informational message to the kernel journal. This means that the message that you write to the kernel journal using the first function will have the journal status of `Info`.

To specify the journal status, you'll have to select one of the `JournalStatus` values after writing your message. This feature is available in the second function overload.

The journal status can be one of:

* `Fatal`: A fatal error has occurred
* `Error`: An error has occurred
* `Warning`: A continuable error has occurred
* `Info`: Just a simple message

</details>

<details>

<summary>Getting journal entries</summary>

You can get all the current session's kernel journal entries by calling the `GetJournalEntries()` function to get these entries with the properties that are explained at the top of this page.

```csharp
public static JournalEntry[] GetJournalEntries() { }
```

</details>

<details>

<summary>Manually saving journals</summary>

To manually save the kernel journals for this session, you can use the `SaveJournals()` function to force saving all the journals to the current session's journal file.

```csharp
public static void SaveJournals() { }
```

</details>

<details>

<summary>Printing the journal log</summary>

The journal management class also provides you an easy way to print the journal log and its details, such as the time, the status, and the message. You can use the `GetJournalEntries()` function to print the log to the console.

```csharp
public static void PrintJournalLog() { }
```

</details>
