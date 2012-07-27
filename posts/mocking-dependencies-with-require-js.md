---
title: Mocking Dependencies For Unit Testing With require.js
date: '2012-07-27'
description: How to mock dependencies to unit-test AMD modules written for require.js.
categories: coding
tags: [javascript, testing, requirejs, AMD]

type: draft
---

I am trying to get a large Backbone app under test, and have been wrestling
with [requirejs](http://requirejs.org) to figure out how to mock dependencies.

Let's say the code for my module looks something like this:

    define(['hurp', 'durp'], function(Hurp, Durp) {
      return {
        foo: function () {
          console.log(Hurp.beans)
        },
        bar: function () {
          console.log(Durp.beans)
        }
      }
    }

How should I mock out `hurp` and `durp` so I can unit test?


## The Solution(s)

I have found three different solutions to this problem, none of them pleasant.

### Defining Dependencies Inline

    define('hurp', [], function () {
      return {
        beans: 'Beans'
      };
    });

    define('durp', [], function () {
      return {
        beans: 'durp beans'
      };
    });

    require('hurpdhurp', function (HurpDurp) {
      // test hurpdurp in here
    });

This is *fugly*. You have to clutter up your tests with lots of requirejs
boilerplate in addition to just defining your mocks.

### Loading Mock Dependencies From Different Paths

This involves using a separate `require.config` to define paths for each of the
dependencies that point to mocks instead of the original dependencies. This is
also fugly, requiring the creation of tons of test files and configurations
files.

### Fake It In Node

This is my current solution, but is still far from ideal.

You create your own `define` function to provide your own mocks to the module
and put your tests in the callback. Then you `eval` the module to run your
tests, like so:

    var fs = require('fs')
      , hurp = {
          beans: 'BEANS'
        }
      , durp = {
          beans: 'durp beans'
        }
      , hurpDurp = fs.readFileSync('path/to/hurpDurp', 'utf8');
      ;



    function define(deps, cb) {
      var TestableHurpDurp = cb(hurp, durp);
      // now run tests below on TestableHurpDurp, which is using your
      // passed-in mocks as dependencies.
    }

    // evaluate the AMD module, running your mocked define function and your tests.
    eval(hurpDurp);

This looks a little funky, but it has a few benefits.

1. Run your tests in node, so no messing with browser automation.
2. Less need for messy AMD boilerplate in your tests.
3. You get to use `eval` in anger, and imagine Crockford's disapproving glare.

It still has some drawbacks, obviously.

1. Since you are testing in node, you can't do anything with browser events or
   DOM manipulation. Only good for testing logic.
2. Still a little clunky to set up. You need to mock out `define` in every
   test, since that is where your tests actually run.

I am working on a test runner to give a nicer syntax for this kind of stuff,
but I still have no good solution for problem 1.

# Conclusion

Mocking deps in requirejs sucks hard. I found a way that sortof works, but am
still not very happy with it. Please let me know if you have any better ideas.
