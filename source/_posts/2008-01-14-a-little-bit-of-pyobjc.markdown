---
layout: post
title: "A little bit of PyObjC"
permalink: /blog/2008/1/14/a-little-bit-of-pyobjc.html
date: 2008-01-14 19:14
comments: true
categories: programming
tags: [iTunesBridged]
---
Well, [Jason][] gave me a bit of a challenge on his [Twitter][], and so
that got me to doing something I’d meant to do for a while.

I’ve wanted to mess around with the new Python bindings, and so I booted
up Leopard and settled in with XCode. My goal was to duplicate a
demonstration of Scripting Bridge that Wolf had done at [PSIG][], except
in [Python][].
<!--more-->
I’ve been a Pythonista for some time, and I like the interactivity mixed
with the ability to create substantial applications.

What do I think? I really like it. I think my development focus is going
to be on Leopard and beyond, for the excellent combination of Cocoa and
Python it offers.

First off, Scripting Bridge takes all the hassle out of talking to
another application. I’ve worked with AppleEvents for years, and it’s
always been a hassle, building up descriptors, and all the half-baked
helpers that have previously existed.

One thing that’s missing from Scripting Bridge for interpreted languages
is that the introspection can’t see the four character codes for
enumerations. That’s easily solved with a little bit of copy and edit
from the .h file made by sdp, so I include that in the code as a
demonstration.

It’s fun to load up [iPython][] to tinker around interactively with a
scriptable application. iPython has tab completion for expressions, so
it’s easy to find out the names of various scripting commands. Unlike
Objective-C, you can tinker with the expressions interactively until you
get them the way you want them, then put them into your main Python code
in your app. I’ll put up a tutorial showing how to do that later.

So attached, you’ll find the code for iTunesBridged, a Python-based
Cocoa app for Xcode 3.0 and Leopard. It shows the simple use of an application controller, Scripting Bridge,
and Cocoa Bindings.

  [Jason]: http://threeve.org/blog/
  [Twitter]: http://twitter.com/threeve
  [PSIG]: http://rentzsch.com/psig/111
  [Python]: http://python.org
  [iPython]: http://ipython.scipy.org/moin/

