---
template: post
title: What are cookies anyway?
slug: what-are-cookies-anyway
draft: false
date: 2020-07-16T08:00:54.344Z
description: This is a bit of a technically lighter explanation meant for not
  technical people to try to understand what is a cookie and why should you even
  care about it.
category: basics
tags:
  - basics
---
![Photo by Christina Branco on Unsplash](/media/christina-branco-7p-wc2z2ujs-unsplash.jpg "Photo by Christina Branco on Unsplash")

This is a bit of a technically lighter explanation meant for not technical people to try to understand what is a cookie and why should you even care about it.

Disclaimer for technical people, to boil it down, some stuff will be purposely slightly inaccurate, or more reflective of HTTP 1 instead of HTTP 2. But for the sake of understanding why cookie matters or not, it's irrelevant.

## A web server doesn't necessarily remember you

To understand the need for cookies, what you need to know at the beginning, is the fact that every time that you reload a page, the "website" doesn't necessarily know if you reload three times, or you are three different people. By the fact of how HTTP works, every load of a page (and more technically also every image, video, whatever it's in that page) is done in a different "call" and, funny enough, if you're on a train with a mobile phone, it could be asked from multiple different "web addresses".

## But how does a website knows that I'm logged in?

That's a good question, and one of the way of doing it it's with cookies.

One simple way to tell if the same user is requesting multiple pages (you're clicking on a link, you're closing your computer and coming next days) is with a simple trick: at some point in a visit, the website and the visitor are agreeing on a call-sign.

It more or less goes like this:

* Yo, I would like to know the weather
* Sure, can I call you a866c58e-dff8-432b-abed-ee10f9a7fa64?
* Sure, every time from now on that I'm asking you something I will send you a866c58e-dff8-432b-abed-ee10f9a7fa64

Now that you have a "shared secret" between you and the website, the website can recognize you and offer you personalized content.

## So, are you trying to tell me that cookies are good right?

I'm just saying that it's not necessarily an evil thing, but we need to go into a bit of a rabbit hole together.

Remember when I told you that every time that you're loading an image, it's like calling again the website? There is also another point, not everything on your website needs to be stored inside of the same website, it's counter-intuitive at first, but it's how most of the internet is working.

Let's say that you're loading [cutedoggo.net](http://cutedoggo.net), and this website is a list of cute pictures of dogs, the pictures of the dogs are stored on different websites, it could be Facebook, it could be Giphy, it could be everything. So, when you're loading [cutedoggo.net](http://cutedoggo.net), Facebook receives a call that says more or less this:

* Hi, I'm safjhasjfhaskjdfhaskjfh and I'm calling from [cutedoggo.net](http://cutedoggo.net), can I have please that cute picture of that dog?
* Sure safjhasjfhaskjdfhaskjfh, here is your picture

This is called third-party cookies, because, no matter that you're on [cutedoggo.net](http://cutedoggo.net), some company like Facebook already knows that you're logged on Facebook and then if you're asking for content on their platform, not only they know what you requested, but also from which website you did, and that opens the pandora box.

## How it can be used wrong

One of the classical examples is that I'm a company that likes to advertise stuff, I have my images or stuff like that in a lot of websites, for example, I have them in car manufacturer websites, and I know which page you're seeing, so, you're interested in EV, in a range of 20-25k, you're also usually in the city, so I think you want a city car EV, let me present you all your options for EV on the market that you will like as soon as you're on Instagram and Facebook, and why not, I'm also putting it into your GF's feed.

Up until this point, there is nothing evil on it, what raised the problem was that segmentation of you wanting to buy some stuff is not usually that straight forward, and some of the companies are doing a creepy job.

Let's say that I know, because you searched for X, that you're sick with something bad, and there is a pandemic that could wipe you out. Why not starting advertising to the kid, during the cartoons, some magic miracle cures that it's not scientifically approved, or even better, life insurance.

This is at some extend illegal, but that's basically why some regulation started to be in place

## But, why would you create a website that contains third-party cookies?

The answer from a developer perspective is A LOT of reasons.

There are a lot of companies that are helping you with part of the website that, if you would build on your own, it would be between very hard to impossible.

One of the most used services that you can find that it's under fire for privacy reason, for example, is Google Analytics, this is an invaluable tool, that is telling you between other things, how many people visited your website, which page, and how much time did they stayed inside. If you would rewrite everything on your own, you would need to be Google. The downside is that now Google knows what people are watching and for how long, and they can better target you for advertising.

## So, should I consent cookies, or not?

That is your decision, and it can change between websites, also, some websites are giving you the possibility of checking which cookies you want to have.

If you want the maximum of privacy, just allow technical cookies (eg. the ones that are keeping you logged in), and don't check for the advertisement cookies, if you don't care, just allow them all.