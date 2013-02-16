---
title: 'EmberCamp 2013 Recap'
date: '2013-02-16'
description: A recap of EmberCamp 2013, the first conference for Ember.js.
categories: code
tags: ['javascript', 'ember', 'embercamp']

---

Despite having neither actual fires or actual camping, EmberCamp was rad. I
had a few thoughts, and then used some electrons and wafers of silicon to
transform those thoughts into words.

### Ember is ready for production
Ember has been in alpha and beta for a while, with constant breaking API
changes and lots of rough edges. The highlight of the conference was the
[1.0 release candidate announcement](http://emberjs.com/blog/2013/02/15/ember-1-0-rc/).
No more breaking changes! Ember apps that work with 1.0 will work without
modification until 2.0, which basically means you don't have to be a
masochist/early adopter/hipster to use Ember in production.

### Ember Data is not ready for production
If you use Rails, and use the [ActiveModel::Serializers](https://github.com/rails-api/active_model_serializers)
gem, and don't do anything crazy with your models, and are willing to spend
lots of time reading the source, then Ember Data might be a good fit for you.
The promise of having a single canonical representation for server-side data on
the client is seductive. Unfortunately it is seductive in a "sirens trying to
murder you by making you crash into rocks" way, not in a "delicious jelly
doughnut that you finally give in to devouring" way. The API is not stable or
locked down, and there are major conceptual problems that still need to be
thought through and implemented to make Ember Data robust enough for general
use.

The Ember team is aware of this, and I imagine Ember Data will receive a lot
more love after 1.0 is released, so expect it to improve.

### Ember cares about the web
Yehuda Katz spent part of his talk speaking about the unique strengths of the
web. The Ember team wants to make it easy to build apps that are better than
desktop quality by combining the speed and interactivity of native apps with the
accessibility and openness of the web. This means embracing URLs for linking to
each state of your app. The Ember router is designed to give this to you by
default. It also means working with upcoming technologies like
[Web Components](https://dvcs.w3.org/hg/webcomponents/raw-file/tip/explainer/index.html)
and upcoming JavaScript language features like
[ES6 Proxies](http://wiki.ecmascript.org/doku.php?id=harmony:proxies) and
[ES6 Object.observe](http://wiki.ecmascript.org/doku.php?id=harmony:observe) to
make development easier and faster.

Also check out Trek Glowacki's talk about genuinely reusable code
and UI elements. This is still a tough problem to solve, and it is encouraging
to see Ember core people concerned about making the web better.

### The Ember Inspector is amazing and I want to subscribe to its newsletter
Yehuda showed off the Ember Inspector, a plugin for the Chrome developer tools
that makes debugging Ember and its abstractions much easier. You can inspect
controllers by clicking on UI elements that are rendered in their context,
easily check out models and their properties, and avoid the frustration of
endless chains of digging deep through the object graph of Ember internals. It
looks really useful and very impressive.

### It is not scary to contribute to Ember
There are at least two core team members (Trek and Peter) who are responsible
for making Ember easier to understand and contribute to. Peter manages GitHub
issues and Trek is the documentation czar. If you find a bug, there are smart
people willing to help you track it down and fix it. If you find an area that
is hard to understand or poorly documented, there are also smart people willing
to help you make it better.

## Concerns
Or, "Now, with the powers of *constructive criticism*, I summon people who know
lots about Ember to tell me why I am wrong!"

### Ember <3 Rails
The RESTAdapter, the only production adapter that Ember Data ships with, is
optimized for Rails. One of the talks about Ember Data had about as much Ruby
code as JavaScript. Another talk was entitled "Client Side Validations for
Ember", but the talk was about automatically turning Rails ActiveModel
validations in to JavaScript code.

__edit__: Tom Dale pointed out that Rails is an easily-targeted platform since
it can emit JSON in a standard format, while other platforms may not have common
conventions on data formatting.

Ember already has the reputation as the "Rails of the client MVC frameworks,"
and there is a real danger that Ember will become the "Rails client MVC
framework." Why is this concerning? After all, the client has to get data from
somewhere, and Rails is a fine back end to get it from.

The web is amazing partly because it is a meta-platform. HTML, CSS and JS are
general enough that there are dozens or hundreds of different toolchains for
creating apps. This freedom fosters rapid innovation. Tying a client-side
framework like Ember to a server-side framework makes everyone who doesn't use
that framework a second-class citizen and hurt its adoption.

I understand that by targeting some Ember Data features specifically at Rails,
Ember can appeal to a large exisiting community of developers who follow
a common set of conventions. I would love to see (and am working to produce)
more information on writing an Ember Data adapter if the RESTAdapter doesn't
fit.

I would also love to see more examples of Ember applications built by tools
other than the Rails Asset Pipeline or Rack::Pipeline. Trek's
[example app](https://github.com/trek/ember-todos-with-build-tools-tests-and-other-modern-conveniences/)
is a good start, as are efforts like Ryan Florence's [ember-tools](https://github.com/rpflorence/ember-tools).
I hope things continue to improve in this area.

## Summary
Despite these concerns, EmberCamp was a great experience and I hope to be at the
next one. If you are on the fence about Ember, now is a great time to check it
out.

### More Ember notes

[Carlos Cardona](http://twitter.com/cgcardona) took detailed notes about each
session if you want to relive the experience before the videos go up.

## Acknowledgements

Thanks to [Brandon Hayes](http://twitter.com/tehviking),
[Tom Dale](http://twitter.com/tomdale) and [Stanley Stewart](http://twitter.com/fivetanley)
for reviewing this.
