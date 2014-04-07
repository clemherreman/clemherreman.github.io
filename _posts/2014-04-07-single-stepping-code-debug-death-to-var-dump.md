---
layout: post
title: "Single stepping code debug, a.k.a. death to var_dump()"
description: "Beating the shit out of var_dump, echo, die and exit."
category: code
tags: [code]
comments: true
share: true
published: false
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
for more than 10 years now — since 2003 — and it's taken extra-good care by the 
tremendous [Derick Rethans](http://derickrethans.nl/who.html), among other great
pieces of work, like the [MongoDB PHP driver](http://pecl.php.net/mongo).








Apply the `half` class like so to display two images side by side that share the same caption.

{% highlight html %}
<figure class="half">
	<img src="/images/image-filename-1.jpg">
	<img src="/images/image-filename-2.jpg">
	<figcaption>Caption describing these two images.</figcaption>
</figure>
{% endhighlight %}




Apply the `half` class like so to display two images side by side that share the same caption.

{% highlight html %}
<figure class="half">
	<img src="/images/image-filename-1.jpg">
	<img src="/images/image-filename-2.jpg">
	<figcaption>Caption describing these two images.</figcaption>
</figure>
{% endhighlight %}