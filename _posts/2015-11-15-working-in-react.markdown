---
layout: post
title:  "Working In React"
date:   2015-11-15 23:17:33 -0600
categories: react
desc: Learning how to spoof mac addresses
keywords: react, reactjs, web, internet, javascript, design, redux
---
I've recently had the privilege of working to both maintain a few existing React based applications as well as build a couple new ones.

There are a lot of things I really like about working in React. I really like how simple it is to understand the fundamentals of working with the library. To get started I went through the [React tutorial](https://facebook.github.io/react/docs/tutorial.html) and read a few articles about the "React way" of doing things, about how to think in React terms.

On the whole, I have been thoroughly impressed by the stability of the library and the community. That is expected with the kind of backing React has, but it is very appreciated coming from an Ember background where every 6 weeks a new version of the framework is released with lots of changes.

## "Thinking in React"

A react application is composed of Components. These components are initialized in a chain starting with the top level parent component.

So when adding a feature to a react application, you essentially break down the UI elements involved into the smallest pieces that make sense, and nest these under parent components as appropriate considering data flow.

An example:

{% highlight bash %}
StoreResultsData
├── Filters
│   └── PriceFilter
└── StoreResults
{% endhighlight %}

So in this example, the `StoreResults` component is responsible for displaying store results based on user selected filters. However, it does not care about which filters are selected, it cares instead about when it's parent `StoreResultsData` component passes it new store results to display.

Likewise, the `Filters` component doesn't care about what store results match the filters selected.

## State Management

But what happens in the example above if the filters section of the app grows and becomes much more complex over time. It is conceivable that we could be passing the functions for updating filter state for `StoreResultsData` more than 3 or 4 component levels deep.

Managing filter state will eventually become incredibly complex. As a developer, coming back to maintain this type of application requires you to basically re-develop your mental model of how state is managed in the feature and where state changes are made, and at which levels. It becomes a mess.

## Redux

This is where Redux steps in. Redux provides a centralized architecture for managing state in a React application.

Redux provides a central repository for application state, called the "store".

In order to make set state, components dispach "action creators" that they have defined. Actions in Redux are simply wrappers around Redux' `dispatch`. Actions correspond to reducer functions which also must be defined, these are the functions responsible for actually changing state, and defining what state looks like (this all makes much more sense after looking at some [Redux examples](https://github.com/rackt/redux/tree/master/examples)).

The important thing to understand is that Redux solves a problem for large React applications, where state will inevitably become fragile over time as it grows.

## Smart vs Dumb Components

Lastly, a pattern worth mentioning is the idea of having smart (AKA stateful) and dumb (AKA stateless) components.

Smart components are typically higher up in the component hierarchy. They are responsible for interacting with state and passing necessary stateful info to the dumb components.

Dumb components are primarily concerned with presentation. They are rendered by the smart components.

To read more about this pattern, check out [this article](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0) on the subject.

## Summary

Working with react has been a pleasure so far and I am continually learning more about how to best approach problems with it.

As I grow in the framework, I'll most certainly want to write more about how my understandings and opinions shift, more to come!
