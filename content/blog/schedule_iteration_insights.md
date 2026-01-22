+++
title = "Insights from low fidelity design iteration"
date = 2026-01-21
#updated = 
authors = ["Violet Chan"]
draft = true
+++

We're currently in the early stages of doing design research to understand how attendees interact with a conference schedule: we want to know what information is most crucial to their decision making and what information is safe to omit. As part of that initiative I have been using a process called paper doll where I create a very low fidelity mock up (traditionally out of paper) with the goal of being able to quickly see how people interact with an idea, change it, and see how that change affects people's response to the mock up.

Thanks to the Nten Open Source Fellowship program we have access to a schedule of events from a previous conference so we can test our ideas against real data. However in order to use that real data we need to make our mock ups difitally rather than on paper.

I used pandas to parse and organize the event data we were given
and then used jinja to style it

It took much longer than anticipated because I got stuck a little in analysis paralysis and perfectionism around parsing everything first

it was also hard to tell what parts of the data we needed before we parsed them into something more usable

the sheer volume of events poses a huge design challenge

I didn't take the time to understand jinja as well as I could have

here are some helpful tips i learned
pandas loc indexing
pandas groupby
jinja filtering and indexing

final design of the mockup process