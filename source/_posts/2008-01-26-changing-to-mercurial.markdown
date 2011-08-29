---
layout: post
title: "Changing to Mercurial"
permalink: /blog/2008/1/26/changing-to-mercurial.html
date: 2008-01-26 19:14
comments: true
categories: programming
tags: [mercurial]
---
Thanks to [Dave Dribin][], and his [analysis][] of git vs.
[Mercurial][], I decided to give Mercurial a try.

It turns out I rather like it! I’d been keeping a lot of my work in
[Subversion][], which is a pretty good centralized source code
management system, but the usual way of using it seemed so heavy:
branches and tags and all kinds of operations took big URLs.
<!--more-->
Don’t get me wrong. Subversion has a lot going for it in environments
where development is managed, and central control is a plus. I haven’t,
for instance, thought of a way that Mercurial could protect a repository
against ad-hoc changes from a developer the way a UID/GID protected
repository in SVN can.

Mercurial has a nice localized workflow. `hg init`, and `hg add` and
`hg commit`, and my stuff is version-controlled, no need to
find/make/design a Subversion repo.

It wasn’t that hard to set up Mercurial for nice web browsing, with
decent log and diff displays. You can subscribe to an RSS feed of the
checkins. On-the-fly creation of tarballs is included, just turn them on
with a config option. And I didn’t have to install any extra software to
do it.

So, as a good start, [iTunesBridged][] is in the repository. And there’s
a new [Source][] link in the menu at the top of the page.

Now, I can get on to some of the other neat things I’m working on.

  [Dave Dribin]: http://www.dribin.org/dave/
  [analysis]: http://www.dribin.org/dave/blog/archives/2007/12/30/why_mercurial/
  [Mercurial]: http://www.selenic.com/mercurial/wiki/
  [Subversion]: http://subversion.tigris.org/
  [iTunesBridged]: https://bitbucket.org/kamitchell/itunesbridged/overview
  [Source]: http://bitbucket.org/kamitchell/

