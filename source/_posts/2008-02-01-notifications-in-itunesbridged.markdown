---
layout: post
title: "Notifications in iTunesBridged"
permalink: /blog/2008/2/1/notifications-in-itunesbridged.html
date: 2008-02-01 01:05
comments: true
categories: programming
tags: [iTunesBridged]
---
HAS commented that I could track changes to the player state of iTunes
using NSDistributedNotificationCenter.

I’ve gone ahead and made changes to the iTunesBriged code to show how to
do that. Now, whenever iTunes changes state, whether it’s via the
iTunesBridged application or by directly manipulating iTunes, the title
of the Play/Pause button changes and the current track name is listed in
the text box.

As mentioned in that comment, [Notification Watcher][] is a great app
for observing distributed notifications. It made it really easy to
figure out what iTunes was sending and what data was in the userInfo.

Thanks for the comment, and the idea!

[Get iTunesBridged source downloads][], which can be cloned with
Mercurial or downloaded as a tarball.

  [Notification Watcher]: http://www.tildesoft.com/Programs.html
  [Get iTunesBridged source downloads]: http://www.bitbucket.org/kamitchell/itunesbridged/
