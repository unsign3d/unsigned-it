---
template: post
title: Communication between microservices
slug: communication-between-microservices
draft: false
date: 2020-07-01T12:44:00.000Z
description: "Communication between microservices, does and don't "
category: microservices
tags:
  - microservices
featured_image: 'images/pexels-designecologist-1366178.webp'
---
This article was written and published 2020–01–07 on my personal blog, this is a repost

# The problem

Let’s say that you’re developing a software in a monolithic approach and you need to create a new functionality. What you will probably do is to search or define a new “business identity” and from there create what you need. If you need to expose something, you will create appropriate APIs, and if you need something from somewhere else, you will just call that method on that class.

When you’re switching to micro-services, or generally a distributed system, this could get a bit complicated because you will have bits of information everywhere and you will start to have complexity rising.

# “Just call it” approach

Let’s imagine that you have a main system and you want to create for now just a small micro-service that is offloading from the main server a small task that is heavy on load. Typical example of this, could be a PDF generation.

The most cost effective solution probably here could be creating the PDF generation “as a service” with an HTTP API (you have a bunch of choice for the protocol to use, you have REST, \[g]RPC, GraphQL and many others).

If you’re using some server-less platform (like AWS Lambda), you may also have the SDK with method of communication already provided to you. In my experience, usually that is the most reliable method because it’s “optimized” by your vendor. Of course, if you’re not careful and you’re building your software entirely based on a 3rd party SDK and that changes, or you want to change vendor, this is usually a bad idea

# In a more familiar manner

You can think about this method as the traditional “service class” method, you’re delegating something to a class, and you are calling it. This just happens over the network

# Pros

* This is probably the simplest method that you can implement, it’s very junior-friendly and you will not have to explain and/or maintain complex architecture
* It’s probably the method with the less moving parts (since you’re not relying on a 3rd service for maintaining the documentation)
* It’s kinda easy to debug, you can associate a “request id” to the entirety of the request and you can see the whole flow of the request from your customer to the server that presented a problem
* You can implement synchronous call to that server and make the client wait for that request (useful in some cases like payment or image manipulation)

# Cons

* You will need to maintain an API, with versioning
* You will have a strong coupling, since the caller will need to know the existence of the server and how to communicate with it.
* You will need to take into consideration network latency, downstream service being not ready or reliable and everything that comes with and external service, even if the service is internal

# Message driven architecture

This is a huge class of possibilities, here I will just touch the basics and the pros/cons of this approach.

I will create more articles about multiple possibilities of implementing this ideology.

# Change in perspective

If you choose to approach this ideology, you will need to shift from the paradigm of A asking to B something, and maybe B to reply to a more inverse approach. If you have already worked with the observer pattern, this will be more natural.

Let’s take the old example of the invoice PDF generation.

In a traditional architecture you would have the main service creating the invoice and then asking a service to generate the PDF, when the PDF is created you will serve it in some way

In a message oriented architecture you have multiple players.

* **A producer**: a software that create something and “announce it” to the public
* **A consumer**: a software that get the “message” and consumes it
* **A communication middleware / messaging system**: It could be a message queue (RabbitMQ / ZeroMQ), a distributed logging (Apache Kafka) or anything that you can imagine

In the case of the example we will have our main application that **temporarily** acts as a producer and announces to the middleware that the invoice is complete. The pdf generator will listen for messages and will **temporarily** act as a consumer, taking all the information that he needs from the PDF generation and maybe he can also act as a producer and announce to the ecosystem that the PDF is ready (e.g.. you can have another service down the line that will take the PDF and sends it via email)

# Pros

As you can imagine already you will have an **extreme decoupling** between services, if you’re sending enough information to describe the business action, everyone will be able to work without knowing about the consumers internal. This is usually why when you will start to encounter this kind of architectures when the project is expanding and more developers are joining, this is a typical architecture that you put in place to get to team independency

The log of the message could become a source to understand what is happening in your whole ecosystem, you can also take those data and create some analysis

# Cons

* Your communication middleware will become quickly your bottleneck
* Usually you don’t have guaranteed orders on the events, so you will need to create your code to adjust for those situations
* Duplication of similar events
* Difficulty of handling failures (in some cases you may have data loss, in some systems, data loss is actually taken into consideration and the ecosystem is built around it)
* Depending on the complexity of the project you will be unable to understand the full picture of what it’s going on after an action (as soon as you will embrace it, this will not be a problem anymore)

# Why should I use it then if it’s so complicated

**tl;dr** usually it grows better and gives way fewer problems than similar alternatives, most of the problems are already solved for you and there is enough literature to not being afraid

**The long answer**

If you need to have synchronous replies, this method is not the go-to. Just find some method to communicate directly and use it.

If you’re not in a rush and you can do stuff in a more asynchronous way you can have a lot more advantages with this approach. If you have already used the observer pattern you will be more appreciative of this.

Let’s take an example of a payment, as soon as the payment is complete you want to do the following:

* create an invoice
* register somewhere that the user paid for accountancy
* unlock features / start the wearhouse procedure for shipment
* update the CRM system
* update other ERP systems
* update dashboards
* that thing that the other team is working on, but it’s a test, so it doesn’t really work that much
* yeah we wanted also to do some tests, does the team have capacity?

This list of things has a couple of interesting properties:

* everything can be done in parallel
* probably some of these points we don’t even want to know what is happening, and we would like to delegate it to other teams

As soon as you’re publishing in the event pipeline that the payment is complete, you don’t need to care anymore about anything else (if you’re not in charge of the other systems). Also, if you look at the quantity of stuff that you will need to do, you will see that if you parallelize it you may save a lot of time