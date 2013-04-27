---
layout: page
title:
tagline:
---
{% include JB/setup %}

This blogs serves as my soapbox, where I can talk about all of the cool things I've learned and am learning. It has been great to learn about Ruby on Rails and fundamental programming on a professional level over the last year. As the end of my apprenticeship approaches, I look forward to exploring further into the depths of this trade. 

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>


