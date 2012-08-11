---
title: 'badoop: a simple todo list in bash'
date: '2012-08-10'
description: Things? OmniFocus? Chumps. Real programmers use bash to track their todos.
categories: coding
tags: [todo, productivity]
---

Todo apps. People must have lots to do, because there are as many todo apps as
hairs in my neckbeard (many).

Well my neckbeard is about to get another hair, because I have created yet
another todo app. Introducing . . .

## badoop

badoop (bash-do . . . p? It sounded cool, don't look at me like that) is a
simple bash script for managing a todo list. Put it in your `$PATH`, and use it
like so:


```
$ badoop Put badoop up on GitHub
$ badoop Finish blog post about badoop
$ badoop
  • put badoop up on GitHub
  • badoop Finish blog post about badoop
$ badoop -d GitHub
$ badoop
  • badoop Finish blog post about badoop
```

badoop is about ten lines of bash. It can do four things.

1. `badoop` with no arguments lists all todo items.
1. `badoop` followed by anything but a `-d` or `-h` will add that as a todo
    item to your todo list.
1. `badoop -d` deletes any todo items matching the arguments passed in next
1. `badoop -h` prints out a help message.

It doesn't do anything with priorities or sorting or nesting or tagging or
logging or anything. If you are wondering if it has a certain feature, the
answer is no. Frankly, if your todo list is that complicated, you may have too
many things to do. You should use a different todo app, or do less things.

### Where The List is Stored

By default, badoop looks for a `$TODO` environment variable defining a path
to a text file to use as the todo list. If it doesn't exist, it will use
`~/.todo.txt` as the todo list.

### Cloud Storage Woop Woop

[Things 2](http://culturedcode.com/things/) just got cloud storage. Pffffft.
badoop has had this forever.

```
$ TODO=~/Dropbox/todo.txt
$ badoop Tell everyone about my sweet cloud storage.
$ badoop
  • Tell everyone about my sweet cloud storage.
```

Consider it clouded.

### Getting The Code

Badoop is on GitHub. Check out the [code](https://github.com/jergason/badoop),
and contribute if you want!
