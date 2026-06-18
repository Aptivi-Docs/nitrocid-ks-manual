---
description: Handles all your RSS feeds
icon: square-rss
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/fundamentals/simulated-kernel-features/extra-features/more-networking/rss-client
---

# RSS Client

<figure><img src="../../../../.gitbook/assets/image (49) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
As of 0.1.0, this feature has been moved to the kernel addons.
{% endhint %}

RDF Site Summary or Really Simple Syndication (RSS) is a web feed that allows users and applications to get updates from the web sites that support RSS feeds. It consists of elements that contain information about the latest feeds and their summary, date published, title, and so on. It was hugely popular between 2005 and 2006.

The simulated kernel contains the RSS client which gets updates from any RSS feed, as well as list and read the feeds. It automatically synchronizes the feed every set interval. The default interval for the refresh is 1 minute.

***

## <mark style="color:$primary;">Connecting to a feed</mark>

To connect to any RSS feed, get any RSS feed URL and execute the `rss` command with the URL. The usage of this command is `rss [-tui] <feed>`.

***

## <mark style="color:$primary;">RSS feed interactive TUI</mark>

<figure><img src="../../../../.gitbook/assets/image (50) (1).png" alt=""><figcaption></figcaption></figure>

If you passed the `-tui` switch, it'll open the interactive TUI to your favorite RSS feed URL listing all your articles. Here are the controls:

<table><thead><tr><th width="129.99993896484375">Keybinding</th><th>Description</th></tr></thead><tbody><tr><td><code>F1</code></td><td>Shows you more information about the article that you're reading</td></tr><tr><td><code>F2</code></td><td>Opens your web browser to the article</td></tr><tr><td><code>F3</code></td><td>Refreshes the list of articles for new updates</td></tr></tbody></table>
