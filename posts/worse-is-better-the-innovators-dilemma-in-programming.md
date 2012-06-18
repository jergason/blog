---

title: "Worse is better: The Innovator's Dilemma in programming languages"
date: '2012-03-22'
categories: rants
tags: [languages, worse-is-better]
permalink: post/19735607665/worse-is-better-the-innovators-dilemma-in-programming

---

Disruptive innovation is a pattern in discovered in business, but it
also plays out in programming languages.

[The Innovator’s
Dilemma](http://www.amazon.com/Innovators-Dilemma-Revolutionary-Business-Essentials/dp/0060521996)
is about disruptive innovation. Technologies that are cheaper and less
functional than existing solutions are invented and ignored by
established companies, and are sold by new companies to different
markups. Eventually, the new technology improves enough that attracts
customers from the established companies, and the disruptive technology
replaces the previous technology in the market.

Richard Gabriel explores a similar idea in his famous [Worse is
Better](http://www.jwz.org/doc/worse-is-better.html) essay. He describes
two different schools of thought in programming language design: the MIT
style, where designers try very hard to “do the right thing”, even if it
makes implementation difficult or complicated, and the New Jersey style,
where simplicity of design and correctness take a back seat to
simplicity of implementation. A poor, but complete, feature is better
than a perfect but infinitely delayed one. He compares the MIT-style
Scheme and the New Jersey-style C. Since Mr. Gabriel wrote this essay, C
has won the marketshare and mindshare, not Scheme or any other MIT-style
languages.

C has all the characteristics of a disruptive innovation. It started off
as a small, simple language that was dismissed by serious academics or
businesses. It found a new market in the language of Unix. It became
more popular in this market, and eventually grew to overtake the
MIT-style languages in popularity.

This cycle is playing out again with JavaScript. The language was
[designed in a week](http://yui.zenfs.com/theater/crockonjs-2-hd.mov),
and it shows. It has some terrible features, and for a decade most
people writing JavaScript never bothered to learn the language.
Developers in “serious” languages dismiss it as a toy, not suitable for
real work. However, because it runs in the browser, it can serve a
market that no other programming language can reach. As its popularity
has grown, the speed of the V8 JavaScript VM has allowed it to move to
the server ([node.js](http://nodejs.org)), where JavaScript is directly
challenging the more traditional server-side languages for market share.
JavaScript is disrupting programming languages, like C before it.
