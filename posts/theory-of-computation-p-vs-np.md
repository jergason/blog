---

title: "Theory of Computation: P and NP"
date: '2011-04-02'
tags: [computer-science, theory]
categories: theory
permalink: /post/4290908050/theory-of-computation-p-vs-np

---

I am currently studying the theory of computation, which is a
fascinating subject. It turns out that there are some rigorous,
mathematical truths behind computation that can tell us some extremely
interesting things. For example,

1.  Can this problem be solved by computers?
2.  Can this problem be solved in  a reasonable time by computers?
3.  Can I turn this problem into another problem that can be solved (at
    all, or in reasonable time)?

Read on for a beginner’s explanation of P and NP.

P and NP were terms that I heard thrown around quite a lot by
smarty-pants computer programmers, but they never meant much to me until
now. Here is my understanding of P and NP. If I make any gross errors,
please let me know in the comments. (*Note: this explanation requires
you to have a basic understanding of Big O notation. See
[here](http://stackoverflow.com/questions/487258/plain-english-explanation-of-big-o) for
a good explanation.) *

**P is the set of problems that can be solved in polynomial time**(ie
`O(n\^k)` where `k` is some constant)**. NP is the set of problems that can
be verified in polynomial time.** Essentially, if a problem is in P, it
is easy to solve (Theoretical computer science has a weird definition of
easy). If it is in NP, then it is easy to check if a solution is correct
or not, but we haven’t yet found an easy way to solve it. Our current
solutions to problems in NP usually involve brute force exponential time
algorithms with some heuristics thrown in to try to speed things up.

Showing something is in NP doesn’t mean it isn’t in P, but then you get
into the whole P vs NP problem.

Six Degrees of Kevin Bacon is a problem in P: given a graph of people
with edges representing relationships, is there a path of six or less
edges that connects someone to Kevin Bacon? The polynomial time solution
involves  a breadth-first search of the graph, stopping once Kevin Bacon
has been reached or once all paths have six edges.

A good example of a problem in NP is finding the [Hamiltonian
path](http://en.wikipedia.org/wiki/Hamiltonian_path "Hamiltonian path on wikipedia"),
which is the path through a graph that visits each node exactly once. It
is easy to verify - just try it out and reject if any nodes were visited
more than once or if any nodes were missed - but hard to solve.

Why do you care about this? You are working at a hot startup whose
business plan is a mashup of the words social, Rails,
local, crowd-sourced, and jacuzzi-full-of-benjamins. Obviously, it is a
Facebook-killer, and as such, has a graph of profiles connected by
friendships. Well, suppose your non-technical co-founder decides that
the missing feature from your product is an iteration on the “Six
Degrees of Kevin Bacon” idea: He wants to show the world that everyone
on the site is connected together in one gigantic path that goes through
each profile exactly once. “Easy!” you cry, as you look for the
ActiveRecord method that does this for you. Then you remember that this
is an example of the Hamiltonian path problem, which means that VC
dollars will run out long before the path is found. Instead, you
convince him that implementing Six Degrees of Kevin Bacon is a better
idea. Now each user gets a sweet badge on their profile if they are
within six degrees of Kevin Bacon, who is an avid user of your product.

P and NP are fundamental ideas in computer science. I’ll talk about NP
completeness next, and then P (!)= NP. Let me know what you think in the
comments.
