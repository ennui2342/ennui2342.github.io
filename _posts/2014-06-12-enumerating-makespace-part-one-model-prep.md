---
title: "Enumerating Makespace #1 - Model Prep"
excerpt: My build log for Enumerating Makespace - a project to demonstrate every piece of equipment in my local hackerspace
tags:
    - maker
---

![Makespace](/assets/images/makespace.jpg)

I am very fortunate to have one of the best hacker spaces in the country
on my doorstep. [Makespace][] has been open a little [over a
year](http://makespace.org/2014/04/makespace-the-first-year/), and
provides access to a [comprehensive set of
equipment](http://wiki.makespace.org/Equipment) to the local maker
community.

One of the challenges of such a wide choice, is that members don't really
know what's possible with the kit or aren't familiar with materials. So I
am undertaking a project to produce a piece of artwork which will
demonstrate the range of what can be achieved at Makespace.

The piece will be made up of a repeating element fabricated in different
materials. For this I chose a skull as it's a
common practice form in art, is easily recognisable, and renders well
if you only have 3 axis to play with. I found a [high quality skull
model on Grabcad](https://grabcad.com/library/skull-1) which will be
the base model I'll work from.

![Skull](/assets/images/skull.png)
![Skull pattern](/assets/images/skull-pattern.png)
![Skull mould](/assets/images/skull-mould.png)

The first task was to generate a few basic models that I'll need for
fabrication. I used [Meshmixer][] to rotate the model and cut a plane so
that we're only dealing with the face. Next I merged all the parts in
the model (the teeth and jaw were separate) and filled spaces,
such as under the jawbone, by extruding the top plane of the model.
I generated a shell version, a solid version, and using boolean operations
I created a negative for moulding (this took a lot of time to
cleanup - I'd love an easy tool to create moulds from patterns).

In the next part, I'll create the basic forms with the CNC machine,
which is a precursor to being able to use many of the other techniques
available.

[Makespace]: http://www.makespace.org/
[Meshmixer]: http://www.123dapp.com/meshmixer
