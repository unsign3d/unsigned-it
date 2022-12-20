---
template: post
title: Node's (19.1) test runner, initial impressions and opinions
slug: nodes-191-test-runner-initial-impressions-and-opinions
draft: false
date: 2022-11-04T09:05:33.777Z
featured_image: 'images/nguyen-dang-hoang-nhu-cbEvoHbJnIE-unsplash.webp'
---

# Node's (19.1) test runner, initial impressions and opinions

Photo by <a href="https://unsplash.com/@nguyendhn?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Nguyen Dang Hoang Nhu</a> on <a href="https://unsplash.com/s/photos/test?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>

## Note: what I write could be wrong by the time that you read it

At the time of writing (node 19.1), test APIs are to be considered experimental, so what I write could be out of date by the time a new node version will be out

## Intro
At the end of this blog post, you will know what I think about the "new" feature of node, of having a built-in test runner. Refer to the documentation here https://nodejs.org/docs/latest-v19.x/api/test.html

## TL;DR / Conclusions

It's good stuff, but you will probably want to wait before using it, since it might change at any moment.

## How did I tested it
I created a new project with Create React App, and quickly understood that was the worst possible way to test it.
The main difference of the test runner integrated in Node, and something like Jest, is that the test runner, **just does that, nothing more**; so, as some of you might have imagined, I was greeted with syntax errors.

I then created the minimal way that I can think about testing it:
- Create a module that does weird stuff
- Create a consumer
- Create tests for it

## What I liked

**Speed**
The first thing that really hit me, was the sheer speed difference, between the same(-ish, there are some syntactic differences) test was between jest and node directly. The whole test suite (1 file, 2 tests) took ~0.5 seconds on Jest and ~50ms on node.
I know by experience that the vast majority of that time is actually for bootstrapping everything, so that number will look very different on a long list of tests, and I have a feeling that in that case, the speed difference might be less that what I'm suggesting.

**No external dependency needed**
That's it, you call `node --test` and it works, more languages should do it

**It outputs TAP**
[TAP](https://testanything.org/) is a standard protocol for testing suites, also in the case of the node runner, `run` will output a stream that can be parsed by another program.
If you will use directly this test runner, especially coming from something different, like Jest, or Rspec, you might find it different, and you might have mixed feelings about it, but I really feel that this is the right approach for something embedded inside of the language itself.
The explanation why it's a good idea, is that it's simple, both to read for a developer, and for a software to parse it, and output a different visualisation; also you could run something more "flashy" on your personal machine, and run the faster and simpler TAP on the CI/CD in case that you want to do that.

## What I didn't liked

I don't think I've seen anything that I don't like at this point, it does what it's supposed to.

One thing that may throw off some people, is that, because, in my opinion, it's the least opinionated as possible, you will not have any magic that you will have in Jest.
One example is the mocking of dependencies, I'm pretty sure that it will be left out, and it will be up to the developer to choose if doing dependency injection, or use a tool like [Proxyquire](https://github.com/thlorenz/proxyquire) 