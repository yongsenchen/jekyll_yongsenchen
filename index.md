---
layout: page
title: Welcome!
tagline: Knowledge share here!
---
{% include JB/setup %}

## About Me

I'm an software engineer (<https://www.linkedin.com/in/yongsenchen>). I worked
on

- Analog TV
- Digital TV
- BSP
- Security, especially ARM(R) TrustZone(R) technology

Here is basically some of my technical sharing.

If you find anything is wrong, feel free to correct me :-)

## Posts

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
