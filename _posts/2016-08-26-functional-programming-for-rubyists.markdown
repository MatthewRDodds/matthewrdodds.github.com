---
layout: post
title:  "Functional Programming in Elixir"
date:   2016-08-26T07:30:47-04:00
categories: elixir
desc: Exploring Elixir and functional programming as a Ruby developer
keywords: elixir, web, programming, functional programming, phoenix
---
One of the biggest hurdles for a Rubyist coming to Elixir/Phoenix is the functional programming paradigm. It takes awhile to get used to and is a large mind-shift in terms of how to think about programs.

The functional paradigm is [partially responsible](http://blog.plataformatec.com.br/2016/05/beyond-functional-programming-with-elixir-and-erlang/) for some of the great features of Elixir/Erlang.

The tennants of functional programming include:

**Immutability**

Without the immutability of data, concurrency is a nightmare. There has to be some kind of guarantee for data shared between multiple processes. You get this in Elixir. Any possible value in Elixir is immutable. The only way to change the data in a variable is to rebind it completely. There is no `hash.merge!(other_hash)` in Elixir. (Incidentally, there aren't hashes either.)

**Avoiding "side effects"**

In an object-oriented program, you define classes to model behavior and objects to hold state. You pass an object into a method, the method calls another method on the object to change some internal state that you can reference. Is this the best way? Functional programming encourages you to think simply in terms of inputs and outputs.

Some resources:

- [Functional thinking: Why functional programming is on the rise](http://www.ibm.com/developerworks/library/j-ft20/)
- [Immutability](http://miles.no/blogg/why-care-about-functional-programming-part-1-immutability)
- [Data Transformations](http://miles.no/blogg/why-should-we-care-about-functional-programming-part-2-transformations)
- [Summary of functional programming mention from Thoughtworks' radar report](http://www.drdobbs.com/mobile/thoughtworks-eyes-seismic-shift-in-progr/240009675)

**P.S.**

One of the first questions I had when starting with Elixir/Phoenix is if there are no objects, what do models look like?

The answer, it's a [struct](http://elixir-lang.org/getting-started/structs.html)!

{% highlight elixir linenos %}
App.Repo.get(App.User, 1)
%Bugshift.User{
  id: 1,
  email: "matthewrusselldodds@gmail.com"
  ...}
{% endhighlight %}
