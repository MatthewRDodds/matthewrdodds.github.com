---
layout: page
title: This is my blog.
tagline:
---
{% include JB/setup %}

I write code for an educational company in San Antonio Texas where I get to work with the following frameworks and technologies: 

* Ruby on Rails
* Backbone.js
* CoffeeScript

For the past year I've been employed as an apprentice, and it's been a fantastic learning experience. 

This blogs serves as the place where I can talk about all of the cool things I've learned and am learning. As the end of my apprenticeship approaches, I look forward to exploring further into the depths of this trade.

Check out my posts:

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>


