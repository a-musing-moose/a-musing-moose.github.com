---
layout: post
title: Making the consummé of Service Oriented Architecture
---

It is no great secret amongst those I work with that I am a big fan of
Service Oriented Architecture (SOA). I should probably clarify that I equally
an anti-fan of anything that includes the word _enterprise_ in it's description.
So when I SOA I do not mean horribly convoluted Java/.NET monstrosities. I just
mean the breaking down of useful sub-system into separate services that can be
reused easily.

In the past I have extoled the miriad advantages of SOA to anyone who would
listen whether it was a traditional SOA composed of RESTful services or a
an Event Driven SOA using [RabbitMQ](http://www.rabbitmq.com) or
[ZeroMQ](www.zeromq.org) as backbone. Recently however I have come across some
new players who have, in my opnion, done something pretty smart. They have
achieved the consummé of SOA. They have looked at what people writting
applications (or _apps_ as they appear to be called now) actually require
from a backend and you know what? It doesn't appear to be that different from
application to application.  These companies have been focusing on providing
backend services for mobile apps and for the most part these applications don't
really need that much more that a way to manage users, maybe some location
based services, push/email type communications and to store some bits and
pieces. The term _Backend as a Service_ (BaaS) seems to have been coined to
describe these types of offerings and there are now a few on the scene:

* [Parse](http://www.parse.com)
* [Kinvey](http://www.kinvey.com)
* [Appcelerator Cloud Services (ACS)](http://http://cloud.appcelerator.com/)

I'm sure there are plenty more out there but these are the names that just keep
popping up.

The thing I noticed about all these services is that they all break down to your
regular Create, Read, Update, Delete type operations of different types of
resources. So by starting with a simple service that allows you to store
arbitrary objects it is pretty easy to see how you could add a user management
services, or even an email service (a email is just a resource that another
process sends).

At first glance even I sort of dismissed these backend services are kind of
trivial. I do a lot of backend development like a lot of developers I probably
have a disproportionately inflated sense of how complicated the work I do is.
Sure, something things can get really complex but if you actually sit back and
think about it, the vast majority of work basically boils down to _CRUD_ with
maybe some bells and whistles stacked on top of it. So the more I thought
about it the more I realised the power in these sorts of services and just how
much they really could be used for.

So these sort of services are actually pretty neat and can cover the basic
backend needs of most mobile applications. Some even over _code hosting_ where
you can offload some of your processing to their _cloud_ allowing for some
pretty smart backends to be created. Realling distilling down all the
complexity into just the tasty bits you really need. Just like a consommé.

The numbers speak for themselves to. Since
[Appcelerator](http://www.appcelerator.com) released their cloud services just
over a week ago there have been over 7K new projects started that hook up to
their service.

My only real remaining concerns are around the security/accessiblity of storing
my data in _the cloud_ and whilst they purport scalability and the certain can
scale in terms of raw throughput I do still wonder at what point an application
becomes to complex to have it's backend purely based on these services.

This approach to SOA has inspired me somewhat and I am currently throwing
together some expiremental libraries to make writting these sorts of services
easily and should the prove successful I let you all know about them and how
you can build your own cloud services.
