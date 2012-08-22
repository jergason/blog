---
title: Kneser-Ney Smoothing And You
date: '2012-08-22'
description: Kneser-Ney Smoothing is a technique in natural language processing to obtain better approximation of the probability of a sentence being correct.
categories: coding
tags: [nlp, smoothing, computer-science]

type: draft
---

I am secretly (or not-so-secretly) a hopeful computer science wonk. I really
love the awesome things you can do with machine learning and natural language
processing, and am trying to learn more about all of them.

I have been catching up on the
[Coursera natural lanugage processing class](https://class.coursera.org/nlp/class/index),
and am working on implementing
[Kneser-Ney smoothing](http://nlp.stanford.edu/~wcmac/papers/20050421-smoothing-tutorial.pdf)
in my spelling corrector.

This post is mostly my attempt to explain something complicated to myself in
hopes of understanding it better. First, I'll give some background on spelling
correction in general, and then talk about why Kneser-Ney smothing works.

It assumes some basic familiarity with probability theory and Bayesian stats.
[This](http://www.math.dartmouth.edu/~prob/prob/prob.pdf) is a good intro book
on probability theory if you want to learn more.


## Spelling Correction
Modern spelling correction uses probabilities to calculate the probability that
a word is spelled wrong. If the probability is high enough, we assume the word
is misspelled, and produce a list of suggestions that are more probable to be
correct than the original word.

These 

## Bigrams


## Smoothing
Smoothing tries to solve the problem of holes in your data. If you have never
seen a bigram before, then your estimated probability will be zero! Smoothing
helps estimate the probabilities of events that we have never seen before.

Kneser-Ney smoothing uses two main insights in to figure out how much
probability to give to bigrams we haven't seen before.


## Insight The First

First, we discount the raw bigram counts by a specific pre-determined
amount. `0.75` seems fairly standard, but you could tweak this value as the voices
in your head tell you.

This means that if we saw the bigram `hardcore kitten` 10 times in our training
data, we would say we only saw it 9.25 times. This effectively removes
some probability from every bigram. We have to account for this probability
somehow. How do we decide where to put it?

## Insight The Second

Second, we add back the probability we removed earlier based on how likely a
word is to occur as a novel continuation.

### What is a Continuation?
I hear the "wat" echo from across the internet. A continuation is a bigram
ending in a specific word. The continuation count of a word is how many different
words it follows. An example to the rescue!

Say we are looking at a corpus and find all the occurences of the word 'cannon'.


* ship's cannon
* potato cannon

Say we are analyzing data form memes. The word 'hurp' might appear relatively
frequently.
