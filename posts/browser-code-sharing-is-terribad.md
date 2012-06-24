---
title: Browser Code Sharing Is Terribad
date: '2012-06-21'
description: Sharing code for the browser is terribad.
categories: coding
tags: [javascript, code-sharing, client]

---

[node.js](http://nodejs.org) has the best package management and code sharing
I have ever used. [npm](http://npmjs.org) is amazing. Coming from Ruby, which
needs RubyGems, Bundler, *and* RVM (all of which are great, don't get me wrong)
to sanely manage dependencies across multiple projects, npm gets everything
right.

This post isn't about things that are awesome and sane and right. It is about
something that is painful and terrible and wrong. Sharing code for the browser
sucks. Its suckiness is even worse because sharing code in node is so good. It
is fluffy unicorns good to the flaming rabid human-sized ant-monsters bad of the
browser.

## Who Cares?

What you make easy affects what people do. Sure, sharing browser code is
*possible*, but how many browser libraries have died inside a project directory
because the author couldn't do something as simple as `npm publish .` to share
them?

Bad client-side code charing also encourages reinventing the wheel. If the
barrier to using someone else's code is high enough, you are more likely to
shrug your shoulders and bang out the code yourself.

## No Browser Code Sharing

The most common way of sharing code for the browser is to not share code for
the browser. Since it is hard, people don't do it. They write code to solve
specific problems in their projects, deploy it, and never make it available to
themselves in future projects or to others solving similar problems.

## Bad Browser Code Sharing

Okay, try to imagine a bad way to share code in the browser. Now run it over
with a tractor and poke some swimming-pool-sized security holes in it. You have
arrived at the most common way of sharing code, which is to *hard-code urls to
3rd-party websites* in your HTML. If that doesn't sound insane to you, repeat
it again. Want to use jQuery in your app? Throw in a
`<script src="http://code.jquery.com/jquery-1.7.2.min.js"></script>` and hope
they never get hacked or go down or have network problems. You never want your
app to break because of someone else's problems.

Some people use GitHub as their own personal CDN, which is sketchy at best.
Linking to a GitHub repo has all of the same drawback as linking to
`code.jquery.com`, but will also get you rate-limited.

<blockquote class="twitter-tweet" data-in-reply-to="215962283627642880"><p>@<a href="https://twitter.com/jergason">jergason</a> we’re not a CDN (and you’ll see a perf hit in doing so). We rate limit you on those blob accesses, too.</p>&mdash; Zach Holman (@holman) <a href="https://twitter.com/holman/status/216150775620046849" data-datetime="2012-06-22T12:48:55+00:00">June 22, 2012</a></blockquote>
<script src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

Dependencies are bad. Dependencies that depend on third-party services to
obtain are terribad.

## More Bad Browser Code Sharing

How about you just download the code you want to share from somewhere
and serve it up locally? That way you control everything. No security problems,
no need to update URLs, no worries that 4chan will hack the third-party site
to replace the script with one that loads pictures of . . . unpleasant things.

**NOPE**

What happens when you want to update a dependency? You search the internet for
where it is hosted, download it, and copy it in to your public directory for
your app. What happens when you want to update twenty dependencies, or, more
likely, the same dependency across twenty projects? Congratulations, you have
just been demoted from software engineer to data entry technician. Manually
downloading code turns you in to a human dependency resolver.


## The Holy Grail of Browser Code Sharing

My ideal tool for browser code sharing looks like this:

* A way to explicitly specify dependencies in a file that is human-readable,
  like a `packge.json` file.
* One command to run that downloads all the external dependencies automatically
  from some central location. I want to type `awesomesauce install` and have
  everything done for me.
* The ability to run in development mode so each js file is loaded separately.
  This eliminates an extra build step and saves lots of headache in development.
* The ability to concatenate and minify all code and dependencies in to one
  file for production.
* Some kind of plugin architecture to support code that uses AMD, CommonJS, and
  nothing at all, since we still haven't agreed on a module syntax.

Ideally this tool would use `npm` somehow, since it already has a standard
package metadata format and thousands of modules that can run in the browser.
It would suck to have to publish to two places if you were developing
platform-agnostic code.


## Bright Shining Lights of Browser Code Sharing

Browser code sharing sucks, but some people are trying to make it better. I
have varying opinions on these tools, but all of them are at least pushing the
idea of easily reusable client-side code.

* [Jam](https://github.com/caolan/jam) - npm-like thing for AMD code.
* [Volo](https://github.com/volojs/volo) - build tool that includes commands to
  add libraries, sortof
* [Browserify](https://github.com/substack/node-browserify) - CommonJS-style
  requires, some node APIs work in the browser
* [Onejs](https://github.com/azer/onejs) - CommonJS-style requires, node
  libraries in browser
* [Pakmanager](https://github.com/coolaj86/node-pakmanager) - more common-js
  requires


How do you feel about client-side code sharing? Do you know of any better
solutions? Tell me on Twitter at [@jergason](http://twitter.com/jergason) or
in the comments.
