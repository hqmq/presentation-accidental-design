## Intro
This is a story about a project that started off sad and terrible and ended up happy and delightful.

I'm really excited to be in Finland. Here's an example of why I am excited to be in Finland.

## Finnish Drivers (1 & 2)
In Finland you have really amazing drivers like Jari-Matti Latvala and Miko Hirvonen.

## American Drivers (1 & 2)
In America our professional race car drivers look like this... and this.

But it could be worse...

## Danish Driver
I could be Danish.

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

