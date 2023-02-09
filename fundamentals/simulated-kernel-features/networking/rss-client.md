---
description: Handles all your RSS feeds
---

# 📰 RSS Client

<figure><img src="../../../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

RDF Site Summary or Really Simple Syndication (RSS) is a web feed that allows users and applications to get updates from the web sites that support RSS feeds. It consists of elements that contain information about the latest feeds and their summary, date published, title, and so on. It was hugely popular between 2005 and 2006.

The simulated kernel contains the RSS client which gets updates from any RSS feed, as well as list and read the feeds. It automatically synchronizes the feed every set interval. The default interval for the refresh is 1 minute.

## Connecting to a feed

To connect to any RSS feed, get any RSS feed URL and execute the `rss` command with the URL. The usage of this command is `rss <feed>`.

## Commands

These below commands allow you to interact with the RSS feed and its updated articles.

* `articleinfo <feednum>`
  * Gets the article information for a specified article feed number
* `bookmark`
  * If the current feed is your favorite, you can use this command to bookmark your feed
* `chfeed [-bookmark] <feedurl/bookmarknumber>`
  * Changes your feed to a specified feed URL. If `-bookmark` is specified, the bookmark number is required
* `feedinfo`
  * Gets the RSS feed info
* `list`
  * Lists all the articles within the feed
* `listbookmark`
  * Lists all the bookmarked RSS feeds and their numbers
* `read <feednum>`
  * Opens the article link on your web browser
* `search [-t|-d|-a|-cs] <phrase>`
  * Gets the article information for a specified article feed number
* `selfeed`
  * Opens the feed selector to select your feed by country
* `unbookmark`
  * Removes the bookmark from the current feed
