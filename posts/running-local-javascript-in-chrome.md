---
title: Running Local JavaScript Files In Chrome
date: '2011-11-15'
tags: [javascript]
categories: coding
permalink: post/12857366951/running-local-javascript-files-in-chrome
---

By default, Google Chrome doesn’t allow you to run JavaScript from your
filesystem. This means that if you are testing a JavaScript only app,
lots of times you have to throw up a server simply to get around this
restriction.

I recently discovered two Chrome command line flags that allow local
JavaScript files to run from local HTML files:

    --allow-file-access

    --allow-file-access-from-files

Now you can test client-side apps without having to start up a server.
