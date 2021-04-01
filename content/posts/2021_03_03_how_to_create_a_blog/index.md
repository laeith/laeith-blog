+++
title = "Do you want to create a blog?"
date = 2021-03-03
+++

Do you want to write an article or two? Sounds great, but one will inevitably face the main problem - where to start?
Turns out there are many ways to start, fortunately most of them seem to have relatively obvious trade-offs.

### Basic requirements

Fom the very start I knew that this must be simple, not only because of my poor web skills but also because I didn't really want to spend much time on the technical side.

I had only a few requirements that can be summed up as:
- Low-effort, mostly works out of the box
- Must be local friendly, I really want to have the content on my disk
- Usable with version control system
- Preferably based on Markdown with basic support for images, syntax highlighting, linking etc.

There are many options out there, starting from a fully featured, ready-to-use platforms like [medium](www.medium.com) with WYSIWYG interface through static-site generators (SSG) and ending with custom DIY solutions.

### Fully featured, hosted solutions - medium.com, dev.to etc.

Probably the most common hosted solution is Medium, there are a few other choices in this category (e.g. Blogger) but they mostly share the same problems. Paradoxically, the main problem with these solutions is that they must somehow make money but running a blogging platform... seems to be a very hard business. Medium launched in 2012 and [apparently seven years later they still can't make it even.](https://www.niemanlab.org/2019/03/the-long-complicated-and-extremely-frustrating-history-of-medium-2012-present/)

Since publishing is free, and they really have to make at least some money to make the business viable they went after readers, either directly or by gathering data about them.
This unfortunately sooner or later leads to questionable decisions, like welcoming readers with such atrocities:

{{ image(src="medium_banner.png", alt="Medium welcoming banner") }}

Not to mention the nagging to download their mobile app, popping social media integrations, *almost* working RSS.

On the upside, theoretically, such platforms should make it easier to promote new blogs, make it easy to reach new audiences.
That's probably a lot of value if one wants to commercialize writing. I would also say that the easy of use for publishers is a huge
benefit - no hosting, not so much tweaking etc. Especially for non-tech-savvy people sounds like a good deal. 

### Static site generator - Gatsby, Jekyll, Zola, Hugo, Pelican and others
This is an interesting niche, looks like static site generators exploded during last decade, there are so many that it's even hard to enumerate them. One can probably find an SSG written in every single popular language, sometimes even a few. It's an almost perfect solution for software engineers and tech tinkerers, it's also this type of software that is probably fun to write (probably the reason for huge population).

Static site generator is an application that creates raw HTML pages from different templates/components. This is a simple alternative to bigger systems such as Wordpress or Drupal. The sheer beauty of such solutions lies in simplicity (given at least basic programming skills), we download a sample theme, create a few Markdown-based articles and press 'generate'. 
A few milliseconds later we get a directory fully of static webpages ready to be deployed, at least in theory.

There are two main distractions faced up-front:
1. Initial configuration
2. Deployment

There is definitely *some* cost that needs to be paid up-front, this is especially true for the configuration part. I'd strongly recommend generators that provide single binaries. It makes it trivial to get everything up and running:

{{ image(src="zola_serve.png", alt="Zola serve") }}

On top of simplicity **we get consistency**, I used to toy a little with Python-based solution "Pelican", getting it up and running tends to be an irregular experience - installing Python, getting pip, getting dependencies and finally running efforts might vary from very straightforward to a multi-hour battle (Python2 clashes with Python3, pip missing/clashes, incorrect dependencies, setting up virtual environments, trying to build old blogs that didn't have version specified...). With single-binary solution we can put it into a repository and forget about all these problems once and for all.

Unfortunately the remaining part of configuration is more time-demanding, picking a starting theme, understanding template engine, doing basic modifications and making sure that everything works (images, syntax highlighting, shortcodes, archive) is a few hours effort at the minimum.

Surprisingly, because the end product we get is a bunch of static files It's trivial to get it up and running in public - the market is big enough to have many quick solutions ready, to name a few: Netlify, GitGub Pages, GitLab Pages... with SSGs having documentation for each major platform - e.g. [Zola for GitHub Pages](https://www.getzola.org/documentation/deployment/github-pages/)

### Fully DYI approach, creating a blog platform from scratch

I believe that unless you're trying to create a feature rich portal with potential of having lots of custom features, at least the size of [Art of Manliness](https://www.artofmanliness.com/) you shouldn't even think about it. Even then it's probably better to start with something dirty and quick, only eventually moving to a custom solution.

Something that I outright crossed as a no-go. There is no way I would be able to justify time spent on creating a blogging platform from scratch, this sounds like a great idea for a 1st year student that wants to be a front-end developer - and I'm not entirely sure about that either.

### Final words

Having evaluated most choices I settled with an SSG - [Zola](https://github.com/getzola/zola), I'm not sure if it's much better than e.g. Hugo as both provide very polished basic functionality and I don't really have any use for the more advanced ones. Hugo is definitely better when it comes to the number of templates readily available, Zola is a much younger project. Ruby fans should take a closer look at [Jekyll](https://github.com/jekyll/jekyll) and Python professionals might be content with [Pelican.](https://github.com/getpelican/pelican/)
Because all of them support Markdown it shouldn't be that hard to switch (assuming simple templates) if something goes wrong.

This might not be the best choice for people that 'just want to start blogging, **right now**', for such people I'd recommend looking into hosted solutions like Medium or Blogger. Yes, they have their problems but sometimes nothing beats ease of use. People, especially programmers tend to underappreciate how much time can be saved with not perfect but perfectly good-enough solutions.

On the other hand static site generators seem to be the best choice for novice, tech-savvy bloggers, especially if they don't really want to make money out of it. So far I'm quite pleased with my choice.
