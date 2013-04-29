---
layout: page
title: This is my blog.
tagline:
---
{% include JB/setup %}

I write code for an educational company in San Antonio Texas where I get to work with the following frameworks and technologies: 

*  Ruby on Rails
*  Backbone.js
*  CoffeeScript
*  TDD

For the past year I've been employed as an apprentice. It's been a pretty fantastic learning experience. 

For this blog I will attempt to log at least one thing I have learned each day for reference later.

Check out my posts:

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>


