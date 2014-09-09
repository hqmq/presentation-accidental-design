## Intro
This is a story about a project that started off sad and terrible and ended up happy and delightful.

I'm really excited to be in Finland. Here's an example of why I am excited to be in Finland.

## Finnish Drivers (1 & 2)
In Finland you have really amazing drivers like Jari-Matti Latvala and Miko Hirvonen.

## American Drivers (1 & 2)
In America our professional race car drivers look like this... and this.

## The Beginning
A few year ago I was working for a company that among other things, put on educational events. Events had a date, a time, a venue and a list of attendees.

The process of marketing the events and signing people up was handled by third party companies that would send us a list of people we should expect at the event.

Eventually sending the list turned into an API call.

## The Problem
One day my boss came to me and said. We need to start accepting registrations from a new company. Can you update the registration system? We just need them to be flagged differently in the database so we can run some comparisons later.

That sounded easy enough. The developer who had written the last implementation had quit so I cloned the git repository and opened it up.

## :'( code
I was greated by a screen like this.

This is just a random snippet of code from the Zend Framework project, the actual code was worse. The method that was responsible for persisting a registration from the database was over 350 lines long with many nested conditionals and loops.

There were no tests.

I reflected on my life. I thought about some of the worst things I have ever done, and I still didn't think that I deserved to be looking at code like this.

## The Deadline
As I was coming to the realization that I was in for a very bad day of programming by boss popped his head back into my office and said, "they actually starting sending us registrations yesterday, how soon can we have the system fixed? Also I'm going to need you to fix all the registrations that got flagged incorrectly."

It was clear that in order to really fix this code I would need tests. In order to writ e the tests I would need sample data from the production environment and some help from someone in the business who was familiar with the registration process. It was also clear that I didn't have that mucht time. So I gritted my teeth and after much swearing I had made the change and I was ~~confident~~ hopeful that I hadn't broken anything.

## Time to Think
For 2 months I thought about what a new registration system would look like. We didn't work on the old system much. It pretty much just ran fine so I never had an excuse to embark on a rewrite, but during that time I found myself trying to describe my idea for a new registration system to my coworkers.

## Buzz Word Description
At first I described my new system to other programmers. I found myself using words like "pipeline", "logs" and "mappings". So what's wrong with this description?

It sounds like a buzzword-filled marketing pamphlet. It doesn't help someone understand _what_ the system does. It is about implementation, not purpose.

One day another coworker asked me about the registration system and luckily for me this coworker was not a programmer.

## Metaphoric Description
I fumbled for words for a few minutes and finally out of nowhere I said, "It will work like a University registration office". And suddenly the conversation smoothed out.

## System Metaphor
This of course relates directly to a well known software design idea. Kent Beck described the System Metaphor in his book "XP Explained". It is the idea that you should be able to describe the behavior of your system in a short story.

But knowing about this design idea isn't what helped me understand my new system.

## Talk To People
What helped me understand my system was talking to other people. The process of describing my system helped me to see it from their perspective.

Talking to different kinds of audiences can yield further benefits because you will have to adjust your description for each audience which forces you to consider their perspective.

## Enough Talk
At this point I was tired to talking about this new registration system. I wanted to get a more concrete idea of what I would build, but there was still no reason to embark on a rewrite. So I started to draw.

## A Bad Diagram
This is an example of my early efforts to draw my system. I was trying to capture the basic flow of an API call to register someone for one of our events.

There are lots of things wrong with this picture, but the biggest problems are:
 * It uses symbols that have nothing to do with my system
 * It mixes high-level concepts like mapping with low-level details like database calls and data encodings
 * It does not describe my system

## Top-Level Diagram
This is a little better. It uses symbols taken from my system metaphor and it only has a few top-level ideas in it. Of course this does not describe much of my system, but it gives me an idea of how to take my big problem and break it into several smaller problems:
* How does the "109c" form get filled out?
* Who processes that form?
* What copies of the form get made and where are they stored?
* What does the response letter look like?

I haven't answered these questions, but I have an idea about how to keep the details of eah of these questions separate, and not let them get mixed up into one big ball of code.

## Zoomed Diagram
Now I can dive into any of my top-level concerns and break them into diagrams of their own.

## Intentional Abstraction
This again matches up with a well-known software design idea. You should have multiple levels of abstraction within your system. There should be just a few objects at the highest level of abstraction, and each other their jobs should be taken care of by more detailed objects.

But once again, I didn't arrive at this design by knowing about abstraction...

## Draw Big, Draw Small
I stumbled upon this abstraction by drawing. I could explore tradeoffs of using one set of top-level abstractions vs another set in a short amount of time.

## Keep Calm and Write Code
The day finally arrived that we needed to change something about the existing registration system. One of our existing vendors was supposed to start sending us a new data field to record some a/b testing so that they could figure out which of their marketing techniques were finding the best demographic for us.

Instead of estimating 8 hours of swearing at the PHP code I estimated 16 hours of building a new system from scratch. The new system would initially only support that one vendor and leave the rest of the vendors on the old system.

## Red, Green, Refactor
I ran rails new, figured out how to connect it to our existing database and got some examples of registrations they would send us by adding some logging to the PHP codebase. I started my red, green, refactor cycle.

## Checklist
I started with the receptionist object. Initially it would only know how to handle accepting new registrations, but we knew that later it would have to handle cancellations and other jobs. Wrote some failing tests, made them pass, moved on.

The translator also went pretty smoothly. I knew what values I needed to record in the database and what values were being sent so again I had a good way to start writing my tests and got them to pass.

When I started implementing the vault where we actually saved all of the database values and related them to one another something terrible happened.

## Crying Unicorn
My tests were passing, but the code for the vault was gnarly. It was only slightly better than the code from the old PHP project. How could this happen to me? I thought I had such a clear idea of how my system would work. How did I not see this coming?

I tried a few different refactorings, but pretty quickly I had to just move on because I only had 16 hours to get a prototype ready.

When I forced myself to move on I got very lucky. As I had tried to refactor the vault I had deleted all of my unit tests because they broke every time I changed something. So I ended up comitting my changes with only a few tests that tested the whole vault in one step.

## Leave A Mess
The truth is that when your shiny new idea meets the real world, it will always grow some warts and lose some of its naive ideas. This is why we stopped trying to fully specify our systems before building them. Of course your project won't be perfect on the first try, but when you have to leave a mess behind you can make sure the mess is isolated and surrounded by some tests.

In this case the fact that I only had tests around the outside of the vault meant that when I came back to it later I could change it very quickly without breaking or re-writing any tests. I could make a new structure once I understood how it should look.

If you haven't seen it you should check out Sandi Metz' awesome talk "Go Ahead, Make a Mess" from RockyMountainRuby 2012.

## Another Fix
We got the prototype out live and got it working pretty quickly. A few weeks later my boss stopped by again and told me that it looked like some of our registrations from an existing vendor were being recorded slightly wrong.

If I fixed the existing PHP code I knew it would cost us around 8 hrs of time and swearing, plus I might break someone else's registrations. So instead I said, let me spend 8 hours in the new system. The only thing different for this vendor was the way they sent the data to us, so I only had to add a mapper for them. It took 2 hours to write the test and get it to pass. That left me 6 hours to cleanup the vault.

## Iterative Refinement
Iterative Refinement is right at the heart of the Agile values. We know we will get things wrong, so we make something small and make it better little by little. I didn't get the vault totally cleaned up in those 6 hours, but I was able to break the problem down into 3 sub-problems:
* Record a new contact with their contact info
* Connect that contact to the vendor that sent it
* Connect that contact to an event

I now had a bit more structure and more find-grained tests for the next time I came back. Once again knowing about abstraction hadn't gotten me a better system, but rather...

## Sleep on It
Taking time away from the problem helped me see it more clearly and leaving a mess with just regression tests made it faster for me to fix the next time I came back.

## Plan For Design Time
We all know that "Big Design up Front" doesn't work. But not designing at all doesn't work either. In this particular project we got very lucky because the pacing of the project put the time for design right in our laps.

In general you have to give yourself time to design throughout the life of your project. Take a little time up front to decide what general structure your project will take. If you need to get part of it done in a crunch, bet deliberate about leaving certain areas messy and change your testing style to support future improvement.

Plan on spending an extra 4-6 hours on each additional feature or refinement for the first several months of a project so that you have time to take new ideas and try them out in the code.

This lets you do your design at the time that you are familiar with the problem and the current implementation. You still have to take the time to design, but you can spread it out over the life of a project so that you don't plan things that never happen.

## Duplication is Cheaper...
In her talk "All the Little Things", Sandi Metz makes a pretty strong statement, but one that resonated with me and with many other rubyists. "Duplication is far cheaper than the wrong abstraction".

I am not qualitified to mince words with Sandi, but I'll modify this quote anyway...

## Almost Anything...
"[Almost anything] is cheaper than the wrong abstraction". In my experience thus far the biggest productivity improvement I have seen on any team is when a system has good tests and has good abstractions. When the abstractions in the code match the ideas of the problem that code is trying to solve it becomes much easier to understand and modify that code without breaking things.

I would urge all of us to take some time throughout the life of our projects to find good abstractions.

## Creativity vs Design Principles
Part of what I learned from this experience is that knowing design principles doesn't make my software better, it just helps me to judge between options. Making better software requires that we generate better ideas, better designs.

Both of these things are important, but for me I had to do more than just read good design ideas. I had to get creative.

## Plan Time for Design
Design of course is not free. It has a cost and spending time on design is not always the right decision. Certainly trying to make all your design decisions up front is a terrible idea, but never doing any design for a system that will need to be maintained long-term is equally terrible.

Instead we should plan and budget time for creativity and design into the whole process of a project.

## Find a Team
This kind of planning and budgeting should not be done individually, it should be a group decision. You should have feedback from your team about when we want to pay the cost of more design and when we don't want to pay that cost.

This means you have to work on a team where people are willing to pay the price of good design. MoneyDesktop Rocks!

## Get Creative
The techniques I talked about in this story are only a few ways that you can get the creative parts of your brain involved in software design. There are many other ways that we didn't talk about today. These specific techniques have worked for me many times since then, but more important than the specific ways you come up with new ideas. Make time and effort to be creative and explore new ideas in your code every day.

## Thinker
"When was the last time you thought hard about something for an hour? A Day? Over the course of a month?" ~Rich Hickey (Hammock Driven Development)

There are lots of things you can do to code faster, but how do you think faster?

We are paid for our ideas.

Lets not be great rough draft authors.

Lets write the best code we are capable of instead of the fastest code we are capable of.

## End
Thank you.
