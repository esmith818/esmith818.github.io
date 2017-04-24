---
layout: post
title:  "The Download Manager"
published: true
date: 2017-04-24 08:00:00
categories: automation htpc usenet
tags: 
---
Managing the file downloads may not be a glorious job, but it is critical to the automated home theater system. The binary newsreader is responsible for taking the index files from the monitoring services, downloading the "blocks", locating any missing pieces, reconnecting all the pieces and returning the completed files to the monitoring apps. It is arguably the most important task since the other services could all be replaced with manual steps. But whether manual or automated, you have to have a downloading tool to retrieve the files.

_This is part of a series of posts on setting up an automated home theater system. There are many ways to accomplish this goal, but this is the one I am currently using and it has made cutting cable a joy._

When I first discovered Usenet, I used [SAB](https://sabnzbd.org/) which is written in Python and works across multiple devices. For the most part it worked very well, but it was a script rather than an "app" and it sometimes had trouble running consistently. I had to launch it as a daemon and set up a task to check and make sure it had not crashed, bringing automation to a standstill. More recently I came across NZBget which is written in C++. It is cross-platform and installs as an app. Auto-updating is easier, it's UI seems cleaner, and so far it seems to be more reliable than SAB. Both worked well, but my current preference is [NZBget](http://nzbget.net/). At the time of writing, I am using version 18.1.

![]({{ site.url }}/assets/article_images/2017-04-24-nzbget/nzbget-settings.png)

Download the version of [nzbget](http://nzbget.net/download/) which matches your platform and install it the same way you would any other app. I added the app to my startup items so that it would always run after a reboot.

Once you have the app running, go to the Settings screen. There are several sections and all should be checked to see what might need to be tweaked for your specific scenario. Depending on which pieces of hardware are managing or storing the files, your setup may diverge from mine. Use these settings as a general reference. I am using a mid-2010 Mac Mini with a 2.66GHz dual core processor and 8 GB of RAM to manage my entire process--from managing to downloading to cataloging to viewing. Sometimes viewing will stutter during a large download, but I will either pause downloads during peak viewing times or decrease the download speed (I am lucky to have gigabit fiber) to reduce processing requirements. Below I provide the settings that I am using, per section.

# Settings

_Note that in the upper, right corner there is a View menu, you can toggle this dropdown to display detailed help information for each section. Nzbget does a pretty good job of explaining what each setting does. The information below is as much to help me remember why I set things the way I did as to help you, the visitor. You may find that reading the help information provided in the software is sufficient in which case you can skip the meat of this entry and move along to the next piece in the automation toolbox._

### Info, System, Web Interface

_These sections are really just for general information and personal tastes in user interface. In the **System** section, I recommend making a backup of your settings once you have them working and before making any changes in the future. I kept all the defaults in the **Web-Interface** section._

### Paths

_Paths need to be setup to instruct nzbget where to find the index files, where to download the blocks, and where to place the finsihed file once all the blocks are assembled._

	MainDir: ~/Development/NZBget
	DestDir: /Volumes/MacMedia1/Usenet/Complete
	InterDir: /Volumes/Internal Storage/Intermediate
	NzbDir: ${MainDir}/import
	QueueDir: ${MainDir}/queue
	TempDir: ${MainDir}/tmp
	ScriptDir: ${MainDir}/scripts
	LogFile: ~/Library/Logs/NZBGet.log
	RequiredDir: /Volumes/MacMedia1,/Volumes/MacMedia2

**Main Dir** is the parent directory for all the tasks nzbget performs (see below). It is NOT where downloaded files are stored. If possible, this path should be on same hard drive that the app is running. Mac and Linux are POSIX systems which is why my path starts with a "tilde" (shorthand for home directory).

**DestDir** is where completed downloads will be moved to when complete.

**InterDir** is where nzbget will download the blocks. This is optional--if you leave this field blank, the app will use **DestDir** for both functions. I opted to use a seprate location because of the note that performance would be improved if an intermediate directory was used on a separate hard drive (in my setup, I have two partitions on the main hard drive and two external drives for storage).

_The next 4 fields apply to the various stages of the download process and are intended to be child directories (sub folders) of **MainDir**._

**NzbDir** is where the monitoring app sends the index file.

**QueueDir** is where index files are stored while waiting there turn to be downloaded.

**TempDir** is for temporary files stored during processing.

**ScriptDir** is where script files are stored. You may have custom scripts that run at any point in the download process or the other services may require scripts of their own to be processed. This is where you would put them.

**LogFile** keeps track of all the activities. You'll likely never use it until the system screws up and then a developer may ask you for them to troubleshoot your problem.

**RequiredDir** is any location that must be available for the entire process of adding a file to your HTPC library to complete successfully. In my setup, movies and TV programs are stored in separate locations so each of these are included here to make sure they are available to the automation process. If they were not, downloaded files would remain in the **DestDir** and I would have to move them manually.

### News-Servers

_The news servers are the usenet providers which host the files you will be downloading. You pay a fee to access files through their service. You can pay a monthly fee for unlimited downloads, or "pay as you go" by buying "blocks" of data which don't expire until you use them. For automation, I find the pay-as-you-go system to be more than adequate, but if you like to download lots of old movies or entire, previous seasons of television shows, a monthly subscription may make more sense for you._

_You can have mulitple servers. Most experiences usenet users will advise that you have an account with 2-3 providers, each on a separate usenet backbone which makes the odds of finding an entire file better. One server will act as your main account with the other 1-2 acting as backup servers. This will be discussed in a separate post._

	Active: Yes
	Name: Astraweb (US)
	Level: 0
	Optional: No
	Group: 0
	Host: ssl-us.astraweb.com
	Port: 443
	Username: XXX
	Password: XXX
	JoinGroup: No
	Encryption: Yes
	Cipher:
	Connections: 20
	Retention: 3000

**Active** is self explanatory. Set it to YES to use the server. You might set this to NO if you have multiple servers and you want to temporarily disable one that has run out of data on a pay--as-you-go plan.

**Name** is your human-readable name to distinguish this server.

**Level** is the priority order for using this server for downloads. The lower the number, the higher the higher the likelihood it will be used to download files. In a scenario where you have a primary account and a backup, you would set the primary to '0' and the backup server to '1'. Nzbget would use the primary server for as much as possible and only resort to the backup for any pieces not found on the main server.

**Optional** should be set to YES only if you expect the service may not connect all the time. By default the app will try a server in a specific level several times before moving on to the next level. If a server is set to NO and can not be reached, it may delay your download.

**Group** is used when you have more than one account on the same server. It lets nzbget know not to try antoher server with the same host if the first is found to not work. Some providers for pay-as-you-go issue a new user for each new block of data which is a good example of where this might be useful. In general, leave the default '0' here to disable grouping.

**Host** is the domain where files will be downloaded from. Your provider will supply this information.

**Post** is also given by your usenet provider. Advanced users may use custom ports if they have special rules set up on their router for port forwarding.

**Username** and **Password** are the values you used for your usenet provider account.

**JoinGroup** is a command some older usenet servers required to access files. Odds are that if you are new to Usenet, this will remain NO.

**Encryption** lets the app know if your connection will be encrypted. This ties in with **Port** above. You should try to use an SSL connection whenever possible for added security. In general, if your provider suggests ports 443 or 563, it is an SSL connection and encryption should be set to YES. If your port is 23, 8080 or almost anything else, encryption will be NO.

**Cipher** is an advanced option for encrypting data on your own. Not all servers support this option. If you are unsure what you are doing, this field should remain blank.

Connections** tell the app how many downloads can occur simultanesouly from the same server. The more concurrent connections, the faster the download assuming you have the necessary bandwidth and your usenet provider allows for that number of connections. Your provider should tell you the max number of connections you may use.

**Retention** indicates how long files are kept by the provider. This is also indicated by the provider. Some will offer large retention periods for older files while others may have very short retention periods. It is important to use a number equal to or lower than your provider offers so that nzbget does not waste time looking for a file on a server that doesn't store files that long.

### Security

_Security is used to define who has access to nzbget. At a minimum, you will want to allow access for yourself as well as the various services that interact with nzbget as part of your automated workflow._

	ControlIP: 0.0.0.0
	ControlPort: 8083
	ControlUsername: XXX
	ControlPassword: XXX
	RestrictedUsername: XXX
	RestrictedPassword: XXX
	Add Username:
	Add Password:
	SecureControl: NO
	SecurePort:
	SecureCert:
	SecureKey:
	AuthorizedIP: 127.0.0.1
	UMask: 1000

**Control IP** is the IP address that nzbget will use for communicating with other services. If your entire workflow happens on one computer, you could put 127.0.0.1 here so that nothing outside the device would have access. In my case, I wanted to be able to access the interface from other computers on my network or from a phone app when away from home. For this reason I am using 0.0.0.0 which lets the app respond to its address on my network (192.198.X.X) or the WAN.

**ControlPort** is the port nzbget listens on. Each service will usually have its own port and most come with defaults. If you don't know what you're doing, you should probable stick with the default. I found that the default was getting a lot of unauthorized attempts and opted to change it to something unique.

**ControlUsername** and **ControlPassword** are the credentials you will use to access the app.

**RestrictedUsername** and **RestrictedPassword** are optional values for a secondary user with limited abilities. I use this for my automated services to connect with nzbget. This way I personally am the only user with admin access.

**AddUsername** and **AddPassword** can be used for additional user access. Perhaps you want to give a friend or a developer access for troubleshooting. I do not have additional users.

**SecureControl**, **SecurePort**, **SecureCert** and **SecureKey** are used if you want access via the internet to be via HTTPS. Note that if you enable this level of security, you will also need to set up customer cert and key files. I do not have a means of creating these files so I opted to be less secure.

**AuthorizedIP** defines any IP addresses that do not require user name and password for access. In my case, only the machine that the app runs on can access the app without credentials. Any other device on network or internet must provide proper credentials.

**UMask** is used to set file permissions for downloaded content. I am not using this feature and leave the default '1000'.

## Categories

_Categories are used to define the types of files being downloaded. Each category might have unique settings for how and where to download its associated files. Your monitoring services may request certain categories be added. In my case, I added one custom category for handling files that I add manually since there will be no service to move them automatically to their final storage location._

	Name: GeekMovies
	DestDir: /Volumes/MacMedia1/Movies
	Unpack: YES
	PostScript: videosort/VideoSort.py
	Aliases:

**Name** is the human readable name for the category.

**DestDir** is where these files should be placed once downloaded. If this is left blank, files will be left in the DestDir listed in the Paths section above.

**Unpack** determines whether the pieces downloaded should be merged into the actual binary complete (as oposed to letting a 3rd party app handle that task).

**PostScript** indicates any scripts that should be run against this file once it downloads. Scripts are placed in SciptDir defined in Paths above. In my case, files added manually run a script that renames the downloaded file.

**Aliases** are any other names that should be handled like the name of the category. As an example, you might have a category named "TV" and have an alias for "HDTV".

## RSS Feeds

_You could set up an RSS feed that monitors when files are added and automatically add them to your download queue. I do not use this feature. It sounds like a way to potentially bypass using monitoring services, but I prefer the custom controls I can apply via these services._

## Incoming NZBs

_This section defines how nzbget should handle index files it receives. I believe I used all the default settings._

	AppendCategoryDir: YES
	NzbDirInterval: 5 seconds
	NzbDirFileAge: 60 seconds
	DupeCheck: YES

**AppendCategoryDir** instructs nzbget whether to use subdirectories for categories in DestDir.
**NzbDirInterval** tells nzbget how often to check for a new index file.
**NzbDirFileAge** lets nzbget know how long an index file should remain unmodified before being processed.
**DupeCheck** indicates whether nzbget should check to see if the index was already run. This way the app doesn't bother trying to download an incomplete file a second time saving you from wasting bandwidth on a corrupt or missing file.

## Download Queue

_This section determines how files are handled once in the queue._

	SaveQueue: YES
	FlushQueue: YES
	ReloadQueue: YES
	ContinuePartial: YES
	PropagationDelay: 0 minutes
	Decode: YES
	ArticleCache: 700 MB
	DirectWrite: NO
	WriteBuffer: 1024 KB
	CrcCheck: YES
	PostStrategy: Balanced
	DiscSpace: 250 MB
	NzbCleanupDisk: YES
	KeepHistory: 30 days
	FeedHistory: 7 days

## Connection

## Logging

## Scheduler

## Check and Repair

## Unpack

## Extension Scripts

## Email

## Logger

## Videosort


	
