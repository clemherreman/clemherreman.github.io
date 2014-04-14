---
layout: post
title: "Single stepping code debug, a.k.a. death to var_dump()"
description: "Beating the shit out of var_dump, echo, die and exit."
category: code
tags: [code]
comments: true
share: true
published: true
---

## What's single-stepping?

![Single stepping debugging](/images/post/debug-step-into.gif)

Single-stepping (or [step-by-step](https://www.youtube.com/watch?v=W0OXEHqH9kc) 
debugging) is a way to control the execution flow of a program, while being 
able to evaluate arbitrary code during so. It means that you can actually **see
your program running, and walk through it**, while being able to examinate every
variable, manually run any method, like an omniscient divinity.

This gives you an invaluable help when trying to wrap your head around a particular
bug, or to understand what a convoluted piece of code is *actually* doing.

## Difference with the beloved `var_dump()`

### Not intrusive

The major difference is that debugging is not intrusive: **you don't
have modify your code to be able to get informations**.

Let me say it again: **without modifying your code**. 

  * Ever commited a `var_dump($foo); die;` and broke <del>the production</del> the build?
  * Ever updated a file on a server, then found you broke the live application because of a misspelled method? Or because the file now belongs to `admin:admin` instead of `apache:http`?
  * Ever scanned through a file to remove all your `echo("I'm here");`?

### A Better UX

#### A (cliché) common debug-loop using `var_dump()`:

  1. Insert `var_dump($foo)`;
  2. Refresh the page
  3. Searching for the output…
  4. Hum, I should have put a `<pre>` on it. Scanning through it.
  5. Hum, I see… `var_dump()` is not on the right place. Where is the next called
  method defined?
  6. I'd better not forget to remove this `var_dump()` when I'm done
  7. Whoops, parse error.
  8. What was I looking for?

#### What you can get

  1. Clic to setup a breakpoint in your favorite IDE
  2. Refresh the page
  3. Your IDE popup
  4. Follow the execution flow. Decide if you enter a method
  	 or just go to the next line of code
  5. Examinate any variable state or method returned value
  6. Hunt and kill that bug

![Inspecting state via debugger](/images/post/debug.gif)

## How?

The main debugger in the PHP world the [Xdebug](http://xdebug.org/). It has been there
for more than 10 years now — since 2003 — and extra-good care is taken of it by the 
tremendous [Derick Rethans](http://derickrethans.nl/who.html), among other great
pieces of work, like the [MongoDB PHP driver](http://pecl.php.net/mongo).

Unlike usual debugging, as with a C-written program, the execution of PHP
usually happens in a remote machine. As such, it's not the developer machine
that controls the execution flow of the directly, but rather the server that 
connects to the developer machine, to signal that the program is executing and
asking when to stop and when to run.

![Visual explaination of debugging](/images/post/dbgp-setup.gif)

<figcaption>
  Source: <a href="http://xdebug.org/docs/remote">Xdebug website</a>
</figcaption>

Notice how the server initiate the full-duplex connection, that will serve to enable
dialog between the IDE and PHP.

## Configuring your environment

### Checklist first:

  1. Use an IDE that handles debugging: [PHPStorm](http://www.jetbrains.com/phpstorm/),
     [Sublime Text](http://www.sublimetext.com/), [Netbeans](https://netbeans.org/) 
     (yes, Netbeans), or even [Vim](http://www.vim.org) or 
     [Emacs](http://www.gnu.org/s/emacs/‎). A more exhaustive list can be found on
     the [Xdebug website](http://xdebug.org/docs/remote)
  2. Have [Xdebug](http://xdebug.org) installed on your PHP. <br/> *Note: I do not recommend
     compiling it by yourself, unless you have some time before you.*

*Quick check to ensure Xdebug is installed:*

{% highlight bash %}
$ php -m | grep xdebug
xdebug
{% endhighlight %}

*Note: don't forget to restart your webserver after installing Xdebug*

### All set? Now to the real configuration part. 

First we need to indicate to your PHP that we want to be able to debug its execution:

{% highlight bash %}
# php.ini (or any other .ini loaded configuration file)
# Bare minimum to enable debug on a PHP running locally
xdebug.remote_enable=1
xdebug.remote_port=9000 # Or any other port that suits you

# If PHP runs in a distant server (like in a Vagrant VM)
xdebug.remote_host = your.dev.machine.ip
# OR
xdebug.remote_connect_back = 1
{% endhighlight %}

`xdebug.remote_host` is more secure, as debugging will only be possible from
the specified IP, pretty much like a whilelist. However, as I usually develop using a VM
and a private network between my host a my VM, I usually go with `xdebug.remote_connect_back`,
which means that Xdebug will provide debugging API to whoever runs an HTTP query.

Please refer to [Xdebug's remote configuration](http://xdebug.org/docs/remote) for finer
tuning.

### Configure you IDE

It depends on the IDE, please refer to their documentation. 
[Here's the PHPStorm one](https://www.jetbrains.com/phpstorm/webhelp/configuring-xdebug.html)

This is really important, as your IDE is reponsible to listening to Xdebug.

*Note: In PHPStorm, don't forget to click on `Run > Start Listen PHP Debug Connections`*

Also, don't forget to **actually place a breakpoint in your code.**

### Trigger debugging

Xdebug is monitoring PHP's execution, looking for specific parameters to trigger connection
to your IDE.

* When running PHP from CLI:

{% highlight bash %}
XDEBUG_CONFIG='idekey=your_ide_session_name' php script-that-will-be-debugged.php
{% endhighlight %}

* When running PHP through an HTTP server

Xdebug looks for specific request GET/POST parameter, or specific cookie. You can
either add `?XDEBUG_SESSION_START=session_name` to your url (`GET` parameter), or use
[PHPStorm's very useful bookmarklet](http://www.jetbrains.com/phpstorm/marklets/) 
to create/delete the cookie triggers.

## TL;DR

* Stop putting randon debug code in your beloved code
* Please use bleeding-edge technology from the 80's
* Enjoy easy, fast, side-effect free<sup>\*</sup> debugging

<sup>\*</sup> <small>Almost side-effet free, depend on what expression you evaluate. Obviously
evaluating a *file_put_contents()* function will have side-effects on the filesystem…</small>

![Debug arbitraty code](/images/post/debug-watch.gif)
