+++
title = "Education"
date = 2021-10-01
+++

I don't really believe in 'Top ten books that every software engineer/person absolutely must read' - nonetheless in the past I did follow a few recommendations/suggestions from far more experienced people, and retrospectively it was a huge time-saver.

Another thing that I don't agree with is that to be a good software engineer one needs to thoroughly understand every abstraction one uses. That's bollocks! One could easily spend half of his adult life e.g. studying CPU architectures - and it still might not be enough, especially when taking into account that it's a moving target. Modern computer science is simply too complex for any human, and that's completely fine, we need to adapt and learn to live with that. Having said that, there is definitely a set of fundamental building blocks that  and concepts that can be used to derive complex systems from.

This contains only positions that I currently view as a significant contribution to my repertoire. It *should not be* treated as a guide how to become a software engineer.
I tried my best to avoid very specialized, in-depth works as such are of marginal use for general population and domain experts would already know them. 

Consider this page 'work in progress', once I get *more time* I'll try to provide the reasoning for each choice. I know it's a little bare bones but hopefully will be useful either way.

Another caveat - there are entire topics missing here, programming languages, hardware books, compilers, security, computer graphics etc. the reason is that I either have very limited expertise there or I'm simply not interested in a topic at all.

In no particular order:

**Operating systems:**
- [Operating Systems: Three Easy Pieces by Remzi H. Arpaci-Dusseau and Andrea C. Arpaci-Dusseau](https://pages.cs.wisc.edu/~remzi/OSTEP/)
- [Computer Science from the Bottom Up by Ian Wenand](https://www.bottomupcs.com/)

**Networking:**
- [Computer Networks: A Systems Approach by Larry Peterson and Bruce Davie](https://book.systemsapproach.org/index.html)
- [Beej's Guide to Network Programming by Brian Hall](https://beej.us/guide/bgnet/html/)

**Algorithms / Data Structures / Mathematics** 

I have love/hate relationship with algorithmic books, one day, hopefully, I'll be able to recommend something reasonable.

**Other:**
- [Google's Site Reliability Engineering book](https://sre.google/sre-book/table-of-contents/)
- Designing Data-Intensive Application by Martin Kleppmann
- Zrozumiec Programowanie by Coldwind Gynvael (Polish honorary mention)


**Java:**
- Effective Java by Joshua Bloch
- Java Concurrency in Practice by Brian Goetz

I don't think it's a good idea to recommend language specific books, in the end it's just a tool - and once we are aware of the above, and have tried a few of them, it's *relatively* easy to jump into a new one and be somewhat productive. Having said that, if someone works mostly in Java it might be worth the time to go through these. Especially Java Concurrency in Practice is a good complementary material to Java Memory Model. While the book is quite old it's still worth its weight, especially with modern computer architectures and distributed environments.

### Publications

In construction, one day.

### **Open education**

I tend to do a course or two yearly, because these are usually quite time-demanding I like to write a short review afterwards, it helps to solidify knowledge and might be useful as a review.

#### **Nand2Tetris aka Build a Modern Computer from First Principles, Part 1 by Shimon Schocken and Noam Nisan (Hebrew University of Jerusalem) @ Coursera**
From the beginning of my programming journey I always had that nudging question, lurking somewhere deep in the back of my mind: **How the does it really work?** I've started with Python, it's a high level language that is superb for being productive while at the same time not being that great with actual computer science, and because of that I never had a chance to toy with a very low level infrastructure.  

Course ratings speak for themselves - it has an average of 4.9 out of 5 based on 450(!) reviews on Coursera. You can watch a short talk about this course by [Shimon Schocken himself on Ted.com](https://www.ted.com/talks/shimon_schocken_the_self_organizing_computer_course).

I always had a vague idea how it might work and why some things are the way they are, but I really lacked hands-on experience with first principles. This course is a real eye-opener when it comes to comprehending how computers work (in a simplistic, comprehensible way). During the course we get a unique opportunity to build a computer for the ground up, in this case it means from defining logic gates in 'almostHDL' up to creating a working assembly-like language and using various input/output simulations. All of it works inside a hardware simulator written in Java, which is provided out of the box.  

Obviously modern CPUs are much, much more complicated but the core idea of a computer can be grasped during the course. Admittedly, it has fully satisfied my curiosity, it struck the perfect balance between details and 'the grand idea'.  
The 2nd part is supposedly much more focused on programming (some compilers writing etc.) and for the time being I left it for later.

#### **Algorithms, Part 1/2 by Robert Sedgewick and Kevin Wayne (Princeton) @ Coursera**

Quite demanding and time-consuming, especially when done early in ones algorithmic journey.

#### **Introduction to Computer Science by HarvardX @ edx.org**
As name suggests, this is an introductory course aka CS50x. This is basically a recording of live lectures held at Harvard by David Malan. It's a very broad course that tackles many, many CS topics, though quite shallowly (I guess that's what one should expect from intro lectures). The quality is superb.

It's just that it looks like I took it too late, most concepts were already known to me, so it was kinda a revision... That I didn't really need at that time. Somewhere in the middle I had an opportunity to work on a nice side project which I eagerly took and never came back to finish it. But like I said, it's a nice introductory to CS (computer science, not really programming).

#### **Advanced Data Structures in Java & Data structures: Measuring and Optimizing Performance by UC San Diego @ Coursera**
These two courses are probably the best way to start one's journey with algorithms that I know about, I remember the tasks being quite fun and engaging - the main idea is to implement a few shortest path algorithms (final ones being A* and Dijkstra's) in different scenarios, one of them was to actually create algorithms that work on real data. They provide a GUI (written in Java) and you continually update it with new functionality each week. You can extract map data of virtually any city using the GUI and if you implement algorithms you can visually see your work - and this seems to be exceptionally rewarding for newbies.

Those are fairly short courses that I would recommend to people with very limited CS knowledge and skills. It also requires some basic Java, but knowing fundamentals should suffice.

The only thing I wasn't impressed with was pace and difficulty level. Anyway, It was worth the time at the time.

#### **And others, that I did too many years ago and hardly remember details:**
* Learn to program: The Fundamentals by University of Toronto @ Coursera.org
* Hardware / Software interface by University of Washington @ Coursera
* Operating systems and systems programming - CS 162 (UC Berkeley) by John Kubiatowicz
* Python for researchers by HarvardX (Jukka-Pekka "JP" Onnela) @ edx.org
* Web development by Steve Huffman @ Udacity
* Other...

