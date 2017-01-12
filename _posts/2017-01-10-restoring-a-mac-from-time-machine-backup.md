---
layout: post
title:  "Restoring a Mac from Time Machine Backup"
date:   2017-01-10
categories: blog
---

I had a chance to replace my 12 inch MacBook (it is an exact same model). I wanted to get the new one to be the exact same sate as the old one, so I chose to restore it from Time Machine backup, which was created with the old one. I had never done before, so I leave a note of what I did here for the record.

Actually, it seems there are several ways restoring a Mac from Time Machine backup, which made me confused. If you don't know which one is the right way for you after googling, I recommend you to contact Apple Support, especially using Apple Support iOS app. I did the restore while asking a support person on it.

## Failure case

First, before using Apple Support, I tried the following, and it failed 👻

- Powered on the new Mac, and set up the used language, keyboard layout, etc. as usual, until "Migration Assistant".
- In "Migration Assistant" page, chose "From a Mac, Time Machine backup. or startup disk". And chose a backup from a list.
- The Mac warned me "Your system needs to be updated" because the macOS version of the new Mac was different from the backup, and it suggested to update the OS version. I chose "Update".

![photo](/assets/2017-01-10/2017-01-10-your-system-needs-to-be-updated.jpg)

- After a while, about 15 mins-ish, an error "The system update failed." is displayed. (I was like, oh come on!)

![photo](/assets/2017-01-10/2017-01-10-the-system-update-failed.jpg)

- I tried the update again, and it failed too. At the moment I opened Apple Support app and started chat with a support person to ask how to restore a Mac from backup properly.

## Success case

The support person was super nice and he explained me what I should do well. He answered my questions very carefully as well. He taught me the right way:

- In my case, I wanted to use Time Machine backup for the exact same model of Mac. "Restore From Time Machine Backup" via macOS Utilities is the right choice.
- So, I canceled "Migration Assistant" and Mac's setup. Powered off the Mac.
- "Restore From Time Machine Backup" is available in macOS Utilities. To get into it, I had Mac run in Recovery mode. You can run Mac in Recovery mode by holding down Command + R key when you power on Mac.

![photo](/assets/2017-01-10/2017-01-10-macos-utilities-page.jpg)

- I chose "Restore From Time Machine Backup" from macOS Utilities menu. That's it! The disk was erased completely and restored from the backup.

![photo](/assets/2017-01-10/2017-01-10-restoring-erasing-macintosh-hd.jpg)

![photo](/assets/2017-01-10/2017-01-10-restoring-restoring-files.jpg)

- Restoring took about one and a half hours for 12 inch MacBook 2016 512 GB. About 80 GB was used.

## TL;DR

Check this Apple Support page: [About macOS Recovery](https://support.apple.com/en-us/HT201314)

One more thing, the support person kindly let me know that if you want to use backup from a Mac to another model of Mac, [Migration Assistant](https://support.apple.com/en-us/HT204350) is the right choice.

Happy restoring a mac from Time Machine backup :)
