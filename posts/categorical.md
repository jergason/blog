---
title: The Categorical Distribution In JavaScript
date: '2012-10-15'
description: How to pick between lots of different things
categories: code
tags: [javascript, statistics]

type: draft
---

The
[categorical distribution](http://en.wikipedia.org/wiki/Categorical_distribution)
is a simple but powerful idea that answers the following question:

How do I pick randomly from many different options, all of which are weighted
differently?

It is a valuable tool in your developer toolkit, and is pretty simple to boot.
With the magic of words and the also magic of JavaScript, I'll walk you through
it. We will also touch on some basic topics in math and probability theory, but
you don't need any background to understand.

I am a humble fruit vendor, vending humble fruit. I have decided that I want to
offer my customers a chance to live on the edge, and provide a service I call
fruitroulette. The customer gives me some money, and I give them a random fruit.
Basically they will be on the Highway to the Danger Zone because the experience
will be so intense.

Lets imagine what this would look like in JavaScript.

```JavaScript
var fruitTypes = ['banana', 'apple', 'peach', 'watermellon', 'mango'];
function pickRandomFruit() {
  var randomIndex = Math.ceil(Math.random() * fruitTypes.length);
  return fruitTypes[randomIndex];
}
```

Here we create an array to draw randomly from, and just pick a random number
from 0 to the length of the array (or `[0,length]` in math). We use that
random number as an index into our array to grab a random fruit.

However, being a shrewd businessman as well as a humble fruit dealer, I realize
that some fruits are more expensive than others. I don't want to be giving out
expensive mangos just as often as cheap bananas (Cheap Bananas is also the name
of my ska band). I need some way of drawing randomly from a bunch of fruit,
but weighted so the cheaper a fruit is, the more likely it is to be chosen.

If you are jumping up and down in your chair, shouting "The categorical
distribution!", you either read the title of the blog post, know this already,
or are internet-clairvoyant. Either way, you are rad. Let's see some example code.

```JavaScript
var fruitTypes = [
  { fruit: 'banana', cost: 0.1 },
  { fruit: 'apple', cost: 0.15 },
  { fruit: 'peach', cost: 0.3 },
  { fruit: 'watermellon', cost: 2 },
  { fruit: 'mango', cost: 1.1 }
];

function fruitScore(fruit) {
  return 1 / fruit.cost;
}
```

We need a cost for each fruit. We also want the fruit to be picked more often
the lower the cost, so we have a little function that inverts the cost to 
return a higher score for cheaper fruit.

We are getting closer, but we still need a way of organizing the fruit so
we can pick randomly from them. What if we arrange them in buckets so that
the larger the score, the larger their bucket, and thus the more likely a
randomly drawn number is to fall into their bucket? Something like this:


`|______fruit1_|_fruit2_|____________fruit3_________|fruit4|`
