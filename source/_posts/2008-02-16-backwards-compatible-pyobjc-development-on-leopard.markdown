---
layout: post
title: "Backwards-compatible PyObjC development on Leopard"
date: 2008-02-16 12:06
permalink: /blog/2008/2/16/backwards-compatible-pyobjc-development-on-leopard.html
comments: true
categories: programming
tags: [Leopard, Python, Tiger, appscript]
---
I’m working on a few programs using [PyObjC][]. Some of the neat cool
stuff will be Leopard-only, but there are some utility programs that I’d
like to have working on Tiger as well.

It’d be nice to do all the development with Leopard running.
<!--more-->
It turns out that Leopard has runtime support for [Python 2.3][] (which
is what ships with Tiger)
in`/System/Library/Frameworks/Python.framework`. Makes sense, because
some programs written with Tiger may be linked to 2.3, and they still
run.

There is no main Python interpreter 2.3, and there aren’t enough pieces
around to build extensions (the include directory is missing).

This makes it rather difficult to install PyObjC 1.4 into Python 2.3,
since it needs to build some support libraries. A Python command would
be nice too.

I came up with a solution, one that will at least allow building pure
Python applications with Python 2.3. Extensions won’t build because of
the lack of an include directory.

I run Leopard from an external drive, so far, and so my Tiger drive on
my laptop was still mounted. And I’d installed PyObjC and [Appscript][]
on it.

Digging around, I found the parts that I need: namely, a Python main
program, and the site-packages directory, which hides in
`/Library/Python/<version-number>`. When I installed PyObjC 1.4 and
Appscript under Tiger, they went into site-packages.

So I copied them from my Tiger volume (named Xoots) like this:

    $ sudo rsync -avP /Volumes/Xoots/Library/Python/2.3/ /Library/Python/2.3/
    $ sudo cp /Volumes/Xoots/usr/bin/python2.3 /usr/local/bin

Now, build with Python 2.3 using the [py2app][] that came with PyObjC
1.4:

    $ python2.3 setup.py py2app -s -d Release build

The `-s` means to build a “semi-standalone” app. The application bundle
will contain only files that are not in the main Python installation.
This works well for this app since the Python 2.3 runtime support is
available in both Tiger and Panther. It keeps the bundle smaller, too,
about 1.2M instead of 10M.

Checking the binaries that were copied into the app bundle (the
bootstrap loader and the extension modules for Appscript and PyObjC)
showed they all were linked to version 88 of libSystem, which is a good
sign that the program will run on Tiger or newer.

Testing showed that my test program indeed runs on Leopard, and a reboot
later, runs on Tiger too!

  [PyObjC]: http://pyobjc.sourceforge.net/
  [Python 2.3]: http://python.org/download/releases/2.3.6/
  [Appscript]: http://appscript.sourceforge.net/
  [py2app]: http://undefined.org/python/py2app.html

