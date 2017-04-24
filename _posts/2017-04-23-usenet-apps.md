---
layout: post
title:  "Usenet Apps"
published: true
date: 2017-04-24 04:00:00
categories: htpc
tags: 
---
You'll need several apps working in tandem to pull files from Usenet. Nowadays you have a choice for practically every aspect of the workflow. While I started with Python-based software, I recently made the switch to apps written in C++. These apps seem to work smoother with less resources and have better support and documentation. You're free to choose alternate options, but I think you'll find the following software to satisfy your viewing needs. Note that only the miscellaneous apps below have a fee. These are also optional. All the required software is free and open source.

_NOTE: The links in the titles lead to their respective sites on internet. The links in the descriptions will take you to relevant posts on this blog site._

## Usenet Downloader: [NZBget](http://nzbget.net/)
[NZBget]({{ site.url }}/automation/htpc/usenet/2017/04/24/download-manager.html) is responsible for downloading the index files (tiny files that tell the app where to find a binary file on Usenet) and merging the small "blocks" into a single file suitable for viewing.
<br />_Honorable mention: [SABnzbd](https://sabnzbd.org/)_

## Series Manager: [Sonarr](https://sonarr.tv/)
Sonarr manages your collection of TV shows. You tell it which series to track and then it monitors the indexing sites for new content. When it finds something that matches your criteria (name, quality, language, etc), it automatically downloads the index file and submits it to NZBget.
<br />_Honorable mention: [SickBeard](http://www.sickbeard.com/)_

## Movie Manager: [Radarr](https://radarr.video/)
Radarr is to movies what Sonarr is to television. Note that it only searches for **new** releases which means it is intended for building a list of movies yet to come out. If you want to grab older movies, you're usually better off doing a manual search on an index site.
<br />_Honorable mention: [CouchPotato](https://couchpota.to/)_

## Media Server: [Plex](https://www.plex.tv/)
Plex is the media manager. You'll run the server software on your home theater PC. You'll also install clients on any device(s) you want to use to view the content. I run both server and player software on my HTPC, and have additional clients for Android and Roku.
<br />_Honorable mention: [Kodi](https://kodi.tv/)_

## Miscellaneous
[HandBrake](https://handbrake.fr/) is useful if you have optical disks that you want to add to your digital library.
<br />[NZB360](http://nzb360.com/) is a must have Android app that can manage your automated workflow rom anywhere. There's nothing better than hearing about a new show at the water cooler or coffee shop, and adding it on the spot to your setup.