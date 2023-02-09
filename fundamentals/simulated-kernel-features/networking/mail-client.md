---
description: Manage your messages with this mail client
---

# 📧 Mail Client

<figure><img src="../../../.gitbook/assets/testmail (1).png" alt=""><figcaption></figcaption></figure>

E-mails are used to send messages electronically to different contacts using the Internet. The IMAP servers are there to manage the messages and receive them, while the SMTP servers are there to handle sending both unencrypted and encrypted messages to a recipient. These servers are authenticated by the e-mail address and its associated password.

The mail client downloads the messages and manages them locally, but interacts with the two servers to actually manage your messages and check for new e-mail by constantly sending requests for new messages.

## Connecting to your mail address

{% hint style="warning" %}
You can no longer sign in to your Google account as of **May 30, 2022**. We'll try to solve this problem as soon as possible.
{% endhint %}

To connect the mail client to your own e-mail address, follow these steps:

1. In the normal UESH shell, execute the `mail <address>` command to provide the credentials needed
2. Wait for a few seconds while your e-mail is being signed in

## Commands

You can interact with the messages found in your account with the below commands:

* `cd <folder>`
  * Changes the current mail directory
* `lsdirs`
  * Lists all the mail directories associated with your e-mail address
* `list [pagenum]`
  * Lists all the mail messages associated with your e-mail address, optionally specifying the page number
* `mkdir <foldername>`
  * Makes the new directory in your mail address
* `mv <mailid> <targetfolder>`
  * Moves a message by message ID to the target folder
* `mvall <sendername> <targetfolder>`
  * Moves all the messages from the sender name to the target folder
* `read <mailid>`
  * Reads a message by message ID
* `readenc <mailid>`
  * Reads an encrypted message by message ID
* `ren <oldfoldername> <newfoldername>`
  * Renames the mail folder name to the new name
* `rm <mailid>`
  * Removes a message by message ID
* `rmall <sendername>`
  * Removes all the mail messages sent by a sender
* `rmdir <foldername>`
  * Removes the directory from your mail account
* `send`
  * Sends a message to a recipient
* `sendenc`
  * Sends an encrypted message to a recipient

{% hint style="info" %}
To use the encrypted mail, you need to have both your private key and your recipient's public key. You can manage this by installing [GPG4Win](https://www.gpg4win.org/) or similar software.
{% endhint %}
