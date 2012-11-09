---
title: The Categorical Distribution In JavaScript
date: '2012-10-15'
description: How to pick between lots of different things
categories: coding
tags: [javascript, statistics, math]
---

## Categorical Distributions Are Useful
The
[categorical distribution](http://en.wikipedia.org/wiki/Categorical_distribution)
is a simple but powerful idea that answers the following question:

> How do I pick randomly from many different options when the options have
> different probabilities for being chosen?

When would you ever use this? A few ideas:

* Showing a random post based on number of votes, so more popular posts show up more.
* Simulating random events in a game, where some events are more likely than others.
* Controlling movement of a robot by randomly picking direction based on probabilities of collision

It is a valuable tool in your developer toolkit, and is pretty simple to boot.
With the magic of words and the also magic of JavaScript, I'll walk you through
it. We will also touch on some basic topics in math and probability theory, but
you don't need any background to understand.

## Fruitroulette

I am a humble fruit vendor, vending humble fruit. I have decided that I want to
offer my customers a chance to live on the edge, and provide a service I call
Fruitroulette. The customer gives me some money, and I give them a random fruit.
Basically they will be on the __Highway to the Danger Zone__ because the experience
will be so intense.

Lets imagine what this would look like in JavaScript.

```JavaScript
var fruitTypes = ['banana', 'apple', 'peach', 'watermellon', 'mango'];

function pickRandomFruit() {
  var randomIndex = Math.ceil(Math.random() * fruitTypes.length) - 1;
  console.log("randomIndex is", randomIndex);
  return fruitTypes[randomIndex];
}

console.log("pick random fruit:", pickRandomFruit());
```

Here we create an array to draw randomly from, and just pick a random number
from 0 to the length of the array (or `[0,length]` in math). We use that
random number as an index into our array to grab a random fruit.

## Fruitroulette, Categorical Style

However, being a shrewd businessman as well as a humble fruit dealer, I realize
that some fruits are more expensive than others. I don't want to be giving out
expensive mangos just as often as cheap bananas (Cheap Bananas is also the name
of my ska band). I need some way of drawing randomly from a bunch of fruit,
but weighted so the cheaper a fruit is, the more likely it is to be chosen.

If you are jumping up and down in your chair, shouting "The categorical
distribution!", you either read the title of the blog post, know this already,
or are internet-clairvoyant. Either way, you are rad. Let's see some example code.

```JavaScript
var fruits = [
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


```JavaScript
function createBuckets(fruits, scoreFunction) {
  var scoreAccumulator = 0;
  fruits.forEach(function(fruit) {
    fruit.startScore = scoreAccumulator;
    fruit.endScore = scoreAccumulator + scoreFunction(fruit);
    scoreAccumulator += scoreFunction(fruit);
  });
}
```

This code will create an interval proportional to the score of the fruit. Now
we need one last piece: a function to draw a random fruit.


```JavaScript
function calculateScoreTotal(items, scoreFunction) {
  // Figure out score range
  return items.reduce(function(prevScoreTotal, item) {
    return prevScoreTotal + scoreFunction(item);
  }, 0);
}

function drawFruit(fruits, scoreFunction) {
  var scoreTotal,
      randomScore,
      i;

  scoreTotal = calculateScoreTotal(fruits, scoreFunction);

  // Draw a random score within the range
  randomScore = Math.random() * scoreTotal;

  // Figure out what fruit's bucket the score falls in
  for (i = 0; i < fruits.length; i++) {
    if (fruits[i].startScore < randomScore && fruits[i].endScore > randomScore) {
      return fruits[i];
    }
  }
}

createBuckets(fruits, fruitScore);
console.log("my random fruit is", drawFruit(fruits, fruitScore));
```

This code may look hairy, but it is doing simple things. We need to create
a random number guaranteed to fall within one of the buckets we created. To do
that, we need to know what the range of the buckets is so we can scale the
number returned by `Math.random()`.

Next, we draw a random number within the score range. Then, we just find the
bucket the number falls within, and return the corresponding fruit.

Holy cow, a categorical distribution! We've done it!

## Some Mathy Stuff

Now that we have seen an example in code, I'll explain some of the theory behind
the categorical distribution. If you aren't interested, skip ahead to the next section for a module that
lets you use the categorical in your code. If you want to know more, let's start
with  the definition of a categorical distribution, from
[Wikipedia](http://en.wikipedia.org/wiki/Categorical_distribution):

> [A] categorical distribution [...] is a **probability distribution** that
> describes the result of a random event that can take on **one of K possible
> outcomes**, with the probability of each outcome separately specified.

The first part of the definition tells us that a categorical distribution must
be a probability distribution. Roughly, this means that if you add up the
probabilities of drawing each item from the distribution, they will equal 1.

The second part says that each possible outcome (or fruit, in our case), has a
specific probability of being selected.

Lets confirm that is the case with our distribution.

```JavaScript
var scoreTotal = calculateScoreTotal(fruits, fruitScore);
var probabilitiesForFruits = fruits.map(function(fruit) {
  var scoreRange,
      probability;

  scoreRange = fruit.endScore - fruit.startScore;
  probability = scoreRange / scoreTotal;
  console.log("probability for ", fruit.fruit, " is ", probability);
  return probability;
});

probabilityTotal = probabilitiesForFruits.reduce(function(probTotalSoFar, prob) {
  return prob + probTotalSoFar;
}, 0);

console.log("probability total for all fruits is", probabilityTotal);
```

## Find It On GitHub

If this looks interesting to you, I wrote a little library for working with
categorical distributions in JavaScript. You can find it
[here](https://github.com/jergason/categorical). It does some handy optimizations
to make creating and drawing from the distribution fast.

Also, if math/computer science stuff is cool to you, you should check out the
[Papers in CS](https://groups.google.com/forum/?fromgroups#!forum/papers-in-computer-science)
group. We pick a cool, accessible and foundational paper in Computer Science, 
and meet via Google Hangout to discuss it. It happens about once a month, and
anyone, of any experience level, is welcome. You should join us!

## Further Reading

After finishing this post, I read Keith Schwarz's amazing article called
[Darts, Dice, and Coins](http://www.keithschwarz.com/darts-dice-coins/). It
is basically the Sistine Chapel of writeups on categorical distributions and
algorithms for creating and drawing from them quickly.
