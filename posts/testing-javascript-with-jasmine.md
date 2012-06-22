---

title: Testing JavaScript with Jasmine
date: '2011-10-26'
categories: coding
tags: [javascript, jasmine, testing]
permalink: post/11965353600/testing-javascript-with-jasmine

---

*Being a quick guide on testing JavaScript code with a testing framework
called Jasmine.*

Now that my JavaScript usage has progressed beyond the “Just enough to
use jQuery” level, I decided it was time to start testing it. (Yes, I
should have been doing it before, but better late than never, right?) I
am writing a small module called
[Tolmey](https://github.com/jergason/Tolmey) for dowloading mapping
tiles from a latitudei and a longitude, and needed to test it.

Why Test Your Code?
-------------------

1.  Your code will be better. Code that is easy to test is generally
    easy to use. Code that is hard to test is brittle and harder to use.
    Testing encourages you to think about how someone will actually
    *use* the API you are making, not just if it is correct or not.
2.  You know it is correct.
3.  If you have good enough test coverage, you know what is broken when
    things break. A failing test gives you a reproducible error case,
    which makes debugging and fixing the bug much easier. You can
    refactor with confidence instead of cowering in fear of breaking
    something irreparably.
4.  ? ? ?
5.  Profit

How To Test
-----------

Jasmine is my JavaScript testing framework of choice.
[Jasmine](http://pivotal.github.com/jasmine/). It is modeled after
[RSpec](https://www.relishapp.com/rspec), a testing framework for Ruby.

Jasmine doesn’t assume you are using the DOM. It can handle testing
client-side code, but it is not tied to it. That means you can use the
same testing setup for your client and server-side code, which is nice.

### Initial Setup

**NOTE**: If you already know how to develop npm modules, this will be
mostly review for you. Sorry, but if you want to follow along with the
actual testing part, you need a project that looks like mine.

1.  There are several ways to test your code with Jasmine. I am used to
    just running specs from a command line tool, so the easiest way for
    me was to install
    [jasmine-node](https://github.com/mhevery/jasmine-node). It require
    NPM and Node.js, so make sure you have those installed. Once you do,
    run:

          npm install -g jasmine-node

2.  Now that jasmine-nodes is installed, we need to make sure our
    project we want to test is set up for it. I will walk through
    creating and testing a really simple project that provides a
    function to add “in the bathtub” to strings.

          mkdir bathtub && cd bathtub

    Save this code as `package.json` inside the folder we created:

         {
             "name": "bathtub",
             "description": "All in the bathtub, all the time.",
             "version": "0.0.1",
             "author": "Jamison Dance <jergason@gmail.com> (http://jamisondance.com)",
             "main": "./bathtub.js",
             "keywords": ["bathtub", "awesome"]
         }

    I don’t want to give a full overview of what the `package.json` file
    does, but its basic purpose it to tell JavaScript package managers
    about your code.

3.  Save this file as `bathtub.js` in the same directory:

         (function () {
           "use strict";

           function inTheBathtub(string) {
             return string + " in the bathtub.";
           }

           module.exports = inTheBathtub;
         }());

    This is our JavaScript project. It is a simple function that appends
    ” in the bathtub” to a string that is passed in to it. The
    `module.exports = inTheBathtub;` line lets npm and Ender know that
    when someone types `require('bathtub')`, it should return our
    function.

4.  Now run `npm link` to create a symbolic link between our project and
    the system `node_package` directory. This tells Node.js, and by
    extension jasmine-node, where to find the code for the bathtub
    module.

### Creating And Running Tests

1.  Create a directory to hold your tests. I like to call mine `spec`:

         mkdir spec && cd spec

2.  Create a file named `bathtub_spec.js` in your `spec` directory with
    the following code:

         //Load our function
         var bathtub = require('bathtub');
         describe('bathtub', function () {
           it("should append \"in the bathtub\" to a string", function () {
             var input = "Nothing delights me more than the fine scent of Jarlsberg cheese";
             expect(bathtub(input)).toEqual(input + " in the jacuzzi.");
           });
         });

    Jasmine lets you write tests that read something like English. We
    are describing some functionality of our `bathtub` function. `it()`
    is the actual test that we want to run. We expect our function to
    append ” in the jacuzzi.” to a string we pass in to it.

3.  Run our spec:

         cd ..
         jasmine-node spec/

    If you followed the code exactly, you should see a notice telling
    you that the test failed! This is what my output looks like:

         Started

         F



         bathtub

           it should append "in the bathtub" to a string

           Error: Expected 'Nothing delights me more than the fine scent of Jarlsberg cheese in the bathtub.' to equal 'Nothing delights me more than the fine scent of Jarlsberg cheese in the jacuzzi.'.

             at [object Object].<anonymous> (/Users/jergason/bathtub/spec/bathtub_spec.js:6:28)



         Finished in 0.003 seconds

         1 test, 1 assertion, 1 failure

    Looks like we have a bug somewhere. If you look at the spec, notice
    we are expecting “jacuzzi”, not bathtub. Whoops! Change the
    offending word of the spec to “bathtub” and run it again. You should
    see a message telling you the specs passed.

Further Exploration
-------------------

This simple project was more to set up the environment than to
demonstrate all the functionality of Jasmine. The `toEqual()` method is
a matcher. There are many more that let you test all kinds of things,
and you can add your own if you don’t find one that suits you. See
[](https://github.com/pivotal/jasmine/wiki/Matchers)[https://github.com/pivotal/jasmine/wiki/Matchers](https://github.com/pivotal/jasmine/wiki/Matchers)
for more info about matchers.

That is all for this post. Look out for another post that gets more in
depth into Jasmine and testing.
