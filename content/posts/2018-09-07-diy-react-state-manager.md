---
template: post
title: DIY React state manager
slug: 2018-09-07-diy-react-state-manager
draft: false
date: 2018-09-07T12:44:00.000Z
featured_image: 'images/pexels-designecologist-1366178.webp'
---

## DIY React state manager

This is a tutorial aim to demystify what libraries like react-redux does under the hood and learn about the new context apis

[https://www.pexels.com/photo/woman-holding-white-string-lights-1366178/](https://www.pexels.com/photo/woman-holding-white-string-lights-1366178/)

#### Why even bother

I think there are a couple of reasons why you should be interested in how state management works.

1.  If you know how it works under the hood, a lot of problems that you might have will be more simple to debug, especially if you’re moving away from a consolidated library to a new library which is more edgy you could face some problems
2.  Global state is great but sometimes you don’t want to pollute it for ephemeral things, for example if you have a couple of components that needs to be rendered just in some occasions (loaders, small user stories) you may want to put it put of the global state use the internal state, this has pros (independency) and cons (multiple responsibilities of the component, not clear separation between data and view)
3.  Find new ways to avoid P[rop Drilling](https://blog.kentcdodds.com/prop-drilling-bb62e02cb691) when necessary, after playing around I found new ways to manage my dependencies

#### What does a state manager even do then?

A state management is just a way to move the state from the component to outside of the component. In case you don’t know what a react state management is you can read [this article from Zalando](https://jobs.zalando.com/tech/blog/state-management-react/?gh_src=4n3gxh1).

### Here we go

Few points before starting:

*   The article will follow the code in [this repo](https://github.com/unsign3d/react-context-global-state/)
*   We are using the new [Context Api](https://reactjs.org/docs/context.html),

This is the entry point of everything and we are doing mainly this:

*   We are storing the state (within the component state)
*   We are creating a context provider with some rudimentary APIs
*   We are passing on the consumer

#### The provider

You may have encountered a context provider if you ever set up a react-redux project. The behaviour it’s quite straight forward, every children component will be able to ask for the state. If you’re just using the context api it will be just the context.

If you look at the code you will note that we need to give some features to the basic context provider:

*   Binding of the context to a component state
*   Exposing an api to change the state
*   Basic debugging logs

#### The consumer

The consumer is actually the most boring part of it, you can basically use the Context consumer as is, you just need to include your component and you will have a block with the context.

My dislike for this approach comes from 2 major points

*   Separation between data logic (in this case context) and view logic
*   Future proofing the code, if you want to change to a new state manager you should be able to just change the glue code and not rewriting your components
*   \[bonus\] having a connected object actually gives you much more flexibility and you can combine in one place data from different sources without the component caring where they came from

DISCLAIMER: My implementation is fairly opinionated by react-redux, you can use different patterns

This is the basic implementation of the connect function

And this is the basic usage of the connect function

This is the vanilla React Cat object

There are a few concepts from this 3 pieces of code

*   You can use the “vanilla version” of the context exactly like I created the connect function, the connect function will just DRY out the usage
*   You can map context to props manually, this means that you can add external props and mix them to the context state (as in react-redux)
*   Cat.js is vanilla React, he doesn’t care about how the data got there, he knows what data is from the input and how to use it

### Closing remarks

I hope to have demystified the magic behind what is a state manager and how to use the new Context Api.

I hope that you will also be able to more critical choose which tool is best for you between state manager, context api and just prop drilling

Many thanks to [https://medium.com/@marcopoliefesto](https://medium.com/@marcopoliefesto) for proofreading and giving cool feedback on this article