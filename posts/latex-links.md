---

title: LaTeX URL Links
tags: [latex]
date: '2011-08-11'
categories: coding
permalink: /post/8796053786/latex-links

---

I had a resume. I used a perfectly good Pages template that did
everything for me. I then decided it was an efficient use of my time to
redo it in LaTeX, so I can increase my nerd credibility.

While going about this, I wanted to link to [my GitHub
account](http://github.com/jergason "Jergason's GitHub account") in the
generated PDF. Some googling found the `hyperref` package.

~~~~ {.prettyprint}
\documentclass[12pt,letterpaper]{article}

\usepackage{hyperref}

\begin{document}



Lets all link to my site! How about

just the URL?



\url{http://jamisondance.com}



Looks good. What if we want different anchor text?



\href{http://github.com/jergason/}{Jamison's GitHub Account!}



\end{document}
~~~~

Now off to grow suspenders and a beard.
