---
layout: post
title: "Trying out Bazaar"
permalink: /blog/2008/2/17/trying-out-bazaar.html
date: 2008-02-17 16:52
comments: true
categories: programming
tags: [bazaar, dvcs, git, mercurial]
---
Considering that it’s the “other” DVCS often considered along with
[Git][] and [Mercurial][], I thought I’d give [Bazaar][] a try.

It’s not working out so well so far. I guess I’m too used to Hg; I found
its workflow agreeable.
<!--more-->
Things I miss or annoy me or I haven’t found in evidence so far (feel
free to comment if I’m not understanding something accurately):

-   Named branches in the repo. Bazaar branches == Hg clones. This is a
    big deal to me, I have some projects with several branches that I
    switch between rapidly. In other words, this became part of my
    workflow.
-   Hard linked cloning. Hg uses hard links and copy-on-write. When I
    clone a bzr repo, it’s a copy of everything. So when I have to make
    clones of the repo to get branches, they take just that much more
    space. I can imagine how much space large projects with many open
    branches take on shared server.
-   Instant local http server a la `hg serve`.
-   Hg has RSS feed generators built in to its server and CGI program;
    seems to be an [addon][] for bzr.
-   Not to mention automatic tarball creation for downloads.
-   Specifying the remote bzr command is an environment variable, not an
    option. Inconvenient. Also not in the help for `bzr clone` as a
    consequence.
-   Remote urls are not relative to the log in directory.
-   Come up with a creative and [original][] icon and logo!

My initial take? It’s like losing some of the coolest features of
Mercurial (low overhead cloning, insta web server), and gaining some of
the things I like least of Git (packs…I have to GC my repo?) and
Subversion (branching *has* to use a new repo/storage path?).

I’m sure Bazaar will have wide support. I might use it to see how it
works for offline development of projects in Subversion.

I think for rapid indie development and the web work I do, it’s going to
remain Mercurial. It just fits my workflow better and gives me more
power off the shelf.

  [Git]: http://git.or.cz/
  [Mercurial]: http://www.selenic.com/mercurial/wiki/
  [Bazaar]: http://bazaar-vcs.org/
  [addon]: http://bazaar-vcs.org/FeedGenerators
  [original]: http://www.maccvs.org/

