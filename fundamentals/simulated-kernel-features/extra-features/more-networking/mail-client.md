---
description: Manage your messages with this mail client
icon: envelope
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/fundamentals/simulated-kernel-features/extra-features/more-networking/mail-client
---

# Mail Client

<figure><img src="../../../../.gitbook/assets/image (52) (1).png" alt=""><figcaption></figcaption></figure>

E-mails are used to send messages electronically to different contacts using the Internet. The IMAP servers are there to manage the messages and receive them, while the SMTP servers are there to handle sending both unencrypted and encrypted messages to a recipient. These servers are authenticated by the e-mail address and its associated password.

The mail client downloads the messages and manages them locally, but interacts with the two servers to actually manage your messages and check for new e-mail by constantly sending requests for new messages.

{% hint style="danger" %}
You can no longer sign in to your Google account here in Nitrocid as of **May 30, 2022**. We currently don't have plans to fix this.
{% endhint %}

***

## <mark style="color:$primary;">Connecting to your mail address</mark>

To connect the mail client to your own e-mail address, follow these steps:

{% stepper %}
{% step %}
#### <mark style="color:$primary;">Sign in to the mail shell</mark>

In the normal UESH shell, execute the `mail <address>` command to provide the credentials needed
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Wait for authentication to complete</mark>

Wait for a few seconds while your e-mail is being signed in
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Open the mail TUI (optional)</mark>

You can also use the interactive TUI version of the mail client by issuing the `tui` command inside the mail shell.
{% endstep %}
{% endstepper %}

{% hint style="info" %}
To use the encrypted mail, you need to have both your private key and your recipient's public key. You can manage this by installing [GPG4Win](https://www.gpg4win.org/) or similar software.
{% endhint %}
