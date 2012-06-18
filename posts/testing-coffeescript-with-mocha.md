---

title: Testing CofeeScript with Mocha
date: '2012-05-01'
categories: coding
tags: [javascript, testing, mocha, coffeescript]
permalink: post/22195905500/testing-cofeescript-with-mocha

---


[Mocha](http://visionmedia.github.com/mocha/) is a JavaScript testing
library that is great. It used to just run CoffeeScript out of the box,
but recently they factored support out, probably to support all kinds of
languages that compile down to JavaScript in the future. The result is,
`mocha test/foo.coffee` no longer works.

To get mocha to run test written in CoffeeScript, run the following:

    mocha test/foo.coffee --compliers coffee:coffee-script

Notes to my future self who keeps forgetting this.
