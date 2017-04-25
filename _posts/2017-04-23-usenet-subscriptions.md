---
layout: post
title:  "Usenet Subscriptions"
published: true
date: 2017-04-24 05:00:00
categories: htpc
tags: 
comments: true
---
Usenet is your source for video content in your automated home theater setup. Unlike a P2P system such as torrents, usenet files are uploaded to a cloud-based server where they remain for a set amount of time. Anyone who has an index file that points to the location on the remote server can download it as fast as their internet connection will allow. 

Usenet is comprised of several servers that mirror content. Each server is hosted by a separate provider. This is helpful because it increases the odds of finding the file you are looking for. When a provider is asked to remove a file, they usually just remove a dozen or so "blocks" of the entire file. A file may be made up of around 100 blocks (smaller blocks are easier to download) but removing even 1 makes it impossible to "re-assemble" the pieces into a single file. However, if each provider randomly selects the blocks marked for deletion, you and I can access accounts from each provider to locate the missing blocks from another provider. My understanding is that there are [eight main providers](https://www.reddit.com/r/usenet/wiki/providers#wiki_usenet.farm) with the rest being resellers for one of these primary branches. Having accounts on multiple branches increases the odds of retrieving your file.

Automation also increases your chances of getting complete files. When files are first posted, it takes time for authorities to locat them to request removal. With automation, you can grab the files as soon as they are posted and prior to being marked for deletion. This is why it is typically harder to find older files than more recent ones.

The third way to get around the problem of missing files is to use index files from private indexing sites. An indexing site generates tiny files (usually 2-3 KB) with details on where binary files exist on Usenet. You can either manually search the index of files or have a manager app review RSS feeds from the index sites for the content you're seeking. All indexing sites post index files for files plainly named when posted to Usenet. But users may also upload files using cryptic file names. These names may look something like `shE3jU22CL*(w@&!KJdh#.mkv` which can not be identified as anything by authorities or providers. The private indexing site knows how to decipher the jumbled string and rename it after you download the file to reflect what it actually is in your media library. This is known as "obfuscating". This reason alone makes it worthwhile to subscribe to a private indexer. Unlike providers, it is not necessarily beneficial to belong to multiple private indexers. If you're a member of a popular service, one should suffice.

### Usenet Providers

That depends partially on your use case. If you plan to download lots of older files (e.g. 80s teen movies, the entire Seinfeld series) you'll probably want a monthly subscription with unlimited usage. Many providers also limit bandwidth for monthly subscriptions so you may want to pay more for higher bandwidth.

If, on the other hand, you plan to download current episodes or recent releases and have a limited number of shows you follow, a block account may be sufficent for you. With a block account, you pay for a set amount of data which doesn't expire. Bandwidth is usually not limited and when you run out of data you buy another block. I go the block route which has worked great for me. Depite following *50+* shows per calendar year and averaging 5 movies per month, it takes about a year to go through blocks on 3 providers at a total cost of $80USD. I have a 1TB primary block and two additonal blocks (500GB, 100GB) used only if something is missing on the primary account.

My three providers are:
_Note many sites use referral links. I do not. I get no reward if you follow these links. I only offer them because I have not had problems with their services._
1. [Astraweb](http://astraweb.com/) - $50 for 1TB
2. [Usenet.Farm](https://usenet.farm/) - $16 for 500GB
3. [TweakNews](https://www.tweaknews.eu/en/usenet-plans) - $16 for 100GB

This gives me three unique branches. Usenet.farm is cheaper than Astraweb per data unit, but has a much lower retention period. TweakNews is expensive compared to the other two but I have never renewed it in over 5 years since I only use it for missing blocks. I consider the higher cost per unit worthwhile for the assurance of rarely dealing with missing blocks.

### Indexing Sites

You can start off with a free site like [usenet-crawler](https://www.usenet-crawler.com/) but you'll likely grow frustrated with it fairly quickly. There are several member only sites but you'll find that they are hard to get into unless you know a current member or catch an open registration period by constantly checking r/usenet on Reddit. I stumbled across [NZBgeek](https://nzbgeek.info/) early on and gladly paid for a lifetime subscription ($30 at the time). I don't think there is a waiting period to register and you can try it free for 30 days to make sure you like it. They have forums that also tackle most of the information I offer here and they have knowledgable moderators on around the clock to answer any questions you might have.

### Next Step

Once you have at least one provider and one indexing site, you're ready to set up your [software]({{ site.url }}/_posts/2017-04-23-usenet-apps.md).