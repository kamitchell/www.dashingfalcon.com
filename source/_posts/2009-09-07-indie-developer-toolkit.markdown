---
layout: post
title: "Indie developer toolkit"
permalink: /blog/2009/9/7/indie-developer-toolkit.html
date: 2009-09-07 15:19
comments: true
tags: [business, c4, indie]
---
I’m at the [C4][] conference, and one of the questions asked of the
panel was what they used for email, hosting, version control, and the
like. The panel had good answers.

Here’s what I’m using.
<!--more-->
**Business name**—Be cool. Get one. Even if you don’t incorporate (which
is probably a good idea; I’ll blog about that when I do it), you sound
like you *are* somebody. One of the biggest highs for me was going to
Cook County Clerk’s office to register the name.

<img src="/images/dash_rgb.gif" alt="Logo" style="float: right"/>
**Logo**—Find a logo designer online, and spend a few bucks. Look for somebody
that’s done work that appeals to your tastes. I used [LogoBee][] to design the
Dashing Falcon logo. $249 got me six designs within the first week and several
updates and tweaks. Turnaround on tweak requests was fast.

**Business cards**–I designed my own in Illustrator from the logo files
I got from LogoBee. Saved them as a PDF and had them printed by
[Overnight Prints][]. Full color with a nice glossy coating.

**Web hosting**—Currently, I’m on [Site 5][]. They’ve been affordable
and reliable. The minor annoyance is that they’ve been killing off my
idle shell programs, like if I leave an Emacs running server-side, while
bouncing to a web client to look at what I’m doing.

Another option is to get a slice. I run a server for a friend on
[Slicehost][], and they’ve been great. I don’t worry about backups,
because my friend pays the small incremental cost of backing up the
entire slice regularly. I’m running [Ubuntu][] Hardy Server there, which
makes it easy to add and update packages with APT.

**Website**—I’m using a Content Management System or CMS: [Drupal][]. It
can handle pages, stories, blogs, even forums. It publishes my site map
to search engines, and offers service links. It’s so good I don’t even
mind it’s written in PHP.

The Apache rewrites that implement the clean URLs won’t rewrite the URLs
of static files, so that would be a possibility for a static,
artistically-designed main page.

**Blog editor**–[MarsEdit][]. Great app, works with Drupal.

**Email**—[Google Apps for your Domain][]. I used to run my own email
server, but found I was spending too much valuable time working on spam
control. Do you have a dedicated full-time IT employee? Since you don’t,
get somebody else to do the hard work for you. Google Apps is free for
small businesses. You can still access your mail via POP and IMAP if you
like. And you also can use Google for your calendar, internal or public
wiki pages, and [Jabber][]-based chat in your domain (I’m
[kevin@dashingfalcon.com][] in Jabber).

I won’t run a mail server for myself or anybody else. Ever. I have
better uses for my time than joining the war between spammers and spam
filters.

**Version control**—I prefer [Mercurial][], but also use [Git][] when
I’m working with an existing SVN repo. ***Use version control.***
Unconditionally. I can’t stress that more. A [DVCS][] is just the right
size for a small business or indie developer; once you get familiar with
one, you’ll never regret the effort of setting up SVN again.

I use version control for everything. I use it for my application
source, my [open source][], my downloads, my website. You can even
incrementally back up dumps of your MySQL database
(`mysqldump --skip-extended-insert` keeps only one insert per line).
Backing up my website involves pulling the changes from Mercurial from
my web host.

Anything you do with anything, check in to your DVCS. With Mercurial,
it’s as easy as `hg init; hg add; hg commit`.

Other suggestions or links to *your* resources? Put them in the
comments!

  [C4]: http://rentzsch.com/c4
  [LogoBee]: http://www.logobee.com/
  [Overnight Prints]: http://www.overnightprints.com/
  [Site 5]: http://www.site5.com/
  [Slicehost]: http://www.slicehost.com/
  [Ubuntu]: http://www.ubuntu.com/
  [Drupal]: http://drupal.org/
  [MarsEdit]: http://www.red-sweater.com/marsedit/
  [Google Apps for your Domain]: http://www.google.com/a
  [Jabber]: http://www.jabber.org/
  [kevin@dashingfalcon.com]: mailto:kevin@dashingfalcon.com
  [Mercurial]: http://www.selenic.com/mercurial/wiki/
  [Git]: http://git.or.cz/
  [DVCS]: http://en.wikipedia.org/wiki/Distributed_revision_control
  [open source]: http://www.dashingfalcon.com/hg/

