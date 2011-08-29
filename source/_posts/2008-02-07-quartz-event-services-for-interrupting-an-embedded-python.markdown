---
layout: post
title: "Quartz Event Services for interrupting an embedded Python"
date: 2008-02-07 03:46
permalink: /blog/2008/2/7/quartz-event-services-for-interrupting-an-embedded-python.html
comments: true
categories: programming
tags: [Python, console, embedded, interpreter]
---
I’ve always thought that Emacs was an interesting editor (development
platform?) since it is extensible in the same programming language it’s
written in: Emacs-Lisp. Not only that, but you can extend it at runtime,
right while you’re using it.

I’ve wondered: What if the same thing could be done with a Python
program on OS X. You could even start with a minimal program, and add
functionality to it while running it, saving the intermediate results to
disk so that the next time you start the program, you start up with all
the state and functionality that was there before.

At the very least, it’d be nice to have a robust Python interpreter
running concurrently and inside of the program under consideration.
<!--more-->
I started with the EmbeddedInterpreter project from [PyObjC 1.4][],
along with parts of the CurrencyConvBinding project so that there’d be
something interesting really going on.

To that I’ve added a class called [InterpreterKeyController][]. This
class runs a thread that has an event tap, which can act upon key
presses “out of band”. In other words, it can evaluate key presses as
they arrive in the process, even if the main thread’s run loop is busy
doing something else. Event taps are available with Quartz Event
Services starting in 10.4.

InterpreterKeyController creates the event tap to take effect when
events arrive in the process; it uses [CGEventTapCreateForPSN][] to do
this, which yields a Mach port.

Then it calls [CFMachPortCreateRunLoopSource][] to make a
CFRunLoopSourceRef, and adds that to the thread’s run loop with
[CFRunLoopAddSource][].

Note that the events themselves don’t arrive in the thread’s run loop as
they would for the main thread. Instead, the run loop source invokes the
callback for the tap.

The main run loop could be busy running the Python interpreter.
InterpreterKeyController’s event tap looks for control-C keypresses, and
safely interrupts the Python interpreter. It’s important to get
[Python’s Global Interpreter Lock][] when doing this to avoid corrupting
the interpreter. The Python interpreter gives up the lock every 100
bytecodes, allowing other threads to run, so the GIL will become
available before too long. The code that does the actual interrupt looks
like this:

{% codeblock lang:c %}
PyGILState_STATE gilstate = PyGILState_Ensure();
PyErr_SetInterrupt();
PyGILState_Release(gilstate);
{% endcodeblock %}

KeyboardInterrupt is always taken on the main thread in Python. Due to
the way EmbeddedInterpreter is written, it runs on the main thread. It
does, in fact, run the main thread’s runloop while Python is blocking on
input, and in between I/O operations to the console.

There’s a little bit of code added to the [PyInterpreter][] module to
turn the InterpreterKeyController on only when evaluating interactive
input. Otherwise, the first control-C typed would issue a
KeyboardInterrupt to the application itself, terminating it!

The end result is a Python console that can be embedded into another
running program with some level of safety: If you run something from the
console that goes into an infinite loop, just press control-C and it
will be interrupted. There is no need to force quit the application, as
was necessary with the stock EmbeddedInterpreter if it became hung up.

This can be demonstrated by typing:

{% codeblock lang:python %}
>>> while True: pass
... 
{% endcodeblock %}

which then places the interpreter in an infinite loop. Pressing
control-C results in:

{% codeblock lang:python %}
Traceback (most recent call last):
File "", line 1, in 
KeyboardInterrupt
>>>
{% endcodeblock %}

One thing to note is that everything in the running program is available
in Python. For instance, the application delegate is automatically
included into the interpreter. Since the currency conversion uses Cocoa
bindings, executing a statement like

{% codeblock lang:python %}
>>> appDelegate.dollarsToConvert=5
{% endcodeblock %}

directly affects the model, with the appropriate text field changing in
the UI, and the calculation is triggered as well.

It is my hope that others will find this useful for more safely adding a
console as a diagnostic tool and to aid in experimentation and diagnosis
during application development.

My testing environment is [Python 2.5.1][] installed on Mac OS X 10.4.11
+ Xcode 2.4.1, with [PyObjC][] 1.4 installed.

You can [browse the source code][] for a project that uses
InterpreterKeyController, where you can also tarballs.

Apple’s developer site has more information on [Quartz Event Services][].

  [PyObjC 1.4]: http://svn.red-bean.com/pyobjc/branches/pyobjc-1.4-branch/
  [InterpreterKeyController]: http://www.bitbucket.org/kamitchell/interpreterkeycontroller/src/tip/InterpreterKeyController.m
  [CGEventTapCreateForPSN]: http://developer.apple.com/documentation/Carbon/Reference/QuartzEventServicesRef/Reference/reference.html#//apple_ref/c/func/CGEventTapCreateForPSN
  [CFMachPortCreateRunLoopSource]: http://developer.apple.com/documentation/CoreFoundation/Reference/CFMachPortRef/Reference/reference.html#//apple_ref/c/func/CFMachPortCreateRunLoopSource
  [CFRunLoopAddSource]: http://developer.apple.com/documentation/CoreFoundation/Reference/CFRunLoopRef/Reference/reference.html#//apple_ref/c/func/CFRunLoopAddSource
  [Python’s Global Interpreter Lock]: http://docs.python.org/api/threads.html
  [PyInterpreter]: http://www.bitbucket.org/kamitchell/interpreterkeycontroller/src/tip/PyInterpreter.py
  [Python 2.5.1]: http://www.python.org/download/
  [PyObjC]: http://pyobjc.sourceforge.net/
  [browse the source code]: http://www.bitbucket.org/kamitchell/interpreterkeycontroller/
  [Quartz Event Services]: http://developer.apple.com/documentation/Carbon/Reference/QuartzEventServicesRef/Reference/reference.html

