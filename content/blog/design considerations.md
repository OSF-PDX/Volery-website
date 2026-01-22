+++
title = "Design considerations we're grappling with"
date = 2026-01-21
authors = ["Violet Chan"]
draft = false
+++

Designing a conference app for general use is not an easy task. Since we're building software to be used by anyone, not just one conference, there's lots of ambiguity that we have to reason around, and build compatibility for. We can't know what someone has been using to plan their conference, and don't want to force their hand; so, we need to design our software to be compatible with anything. We also don't know exactly what sort of data any particular conference has for their events and need to design our system to work  with what we get. We also need to ensure accessibility and usability, we ideally want an out-of-box experience that makes the conference run smoother and cheaper than printing out hundreds of schedules.

# data base abstraction

Currently we've picked Nten Tech Conference as our test case and are prioritizing the client interface. Since we have a specific conference in mind we don't _have_ to be completely generalized. For example if the Nten Tech Conference breaks their conference talks into something like `EVENT_NAME, EVENT_TIME, EVENT_END_TIME, EVENT_LOCATION` we can make our current test version do exactly the same thing. Even though we know that in the future another conference might break their conference events down as `EVENT_TITLE, EVENT_START, EVENT_LENGTH, EVENT_ROOM` where both the names and format are different, doing it for the  specific case and then generalizing lets us work out a lot of the kinks in our system and then adapt it to handle other formats smoothly.

That said, we still have thought ahead and made some early architectural decisions to ensure compatibility. Every organization out there is different and tracks their information differently. Some might store conference information (talks, speakers, times, etc) in a shared spreadsheet, others might use a CRM like SalesForce, others might have their own SQL database. Our goal is to include anybody so we need to find a way to be able to work with all of these options. 

Our current solution is that we create a server with its own internal Postgresql database. Anything that our server wants to know, it gets from its internal database. We than have a translation layer between that internal database and the external database that the conference organizers have already been using. The translation layer can then be swapped out depending on what the external database is. If you use salesforce, use the salesforce translator, if you use a google sheet, use the google sheet translator. This way all the code written for the server only needs to know how to work with one database and doesn't need to be rewritten for every data management system you could use.

In the future, we will probably also use this translation layer system to not only translate between the types of database (eg: SalesForce to Postgresql) but also to create a consistent internal database (eg: EVENT_NAME and EVENT_TITLE both get translated to EVENT_HEAD).

Having this internal database and translation layer also means that for smaller orgs, that don't have a very fast or very large scale data management system, our server gets to stand between them and the large volume of information requests all the conference attendees might make. For example, if an org has been using a small online spreadsheet, everyone asking for its data will probably lag it out. But if they ask our server instead, then it takes the load (without lagging) and can bundle any requests that still need to make it back to the sheet together into larger less frequent requests that are easier to handle.

# Accessibility

Accessibility can be broken down to a visual concern and a technological concern. On the visual side we need to ensure that anything we make is legible: acceptable contrast between text and background, Clear layouts, readable fonts, etc. On the technological side we want to make sure that our app is compatible with assistive technology like screen readers and clickless navigation. 

WCAG has a wonderful set of accessibility guidelines. A key takeaway from WCAG is to make use of semantic HTML tagging so that screen readers know exactly what to read, and keyboard navigation is able to detect interactive elements correctly.

Another design consideration is the size of the screen itself. In the modern era it's safe to assume that our app will be viewed in a mobile web browser or through a downloaded mobile app. In either case, we have to make sure the visuals of our design are still legible on a smaller screen, and we need to figure out how to break information that fits nicely on a sheet of paper, fit on a mobile screen.

That concludes our brief overview of some of the software design concerns we've been working with. We're currently actively building our first iteration and we may shift our planned solutions or the priority of our concerns as we continue.

