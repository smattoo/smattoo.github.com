---
layout: page
permalink: /about/index.html
title: Sagar Mattoo
tags: [Sagar Mattoo]
chart: true
---

{% assign total_words = 0 %}
{% assign total_readtime = 0 %}
{% assign featuredcount = 0 %}
{% assign statuscount = 0 %}

{% for post in site.posts %}
    {% assign post_words = post.content | strip_html | number_of_words %}
    {% assign readtime = post_words | append: '.0' | divided_by:200 %}
    {% assign total_words = total_words | plus: post_words %}
    {% assign total_readtime = total_readtime | plus: readtime %}
    {% if post.featured %}
    {% assign featuredcount = featuredcount | plus: 1 %}
    {% endif %}
{% endfor %}

Thanks for visiting my blog, I'm **Sagar Mattoo**. I am a programmer. In India, back then teenagers of my age were mostly stuck between PCM vs PCB fight (M => engineering vs B => medicine), well I applied the KISS principle:-) to choose the easier route, a much-needed characteristic to be a good programmer.

I believe in CL/CA pipeline, yes you read it right, it's not CI/CD:-). CL/CA stands for continuously learning and continuously applying. Well, the rate at which technology is evolving I am pretty sure to keep up with the pace we as programmers need CL/CA ingrained in us.

I have experience working on Microsoft Azure, C#, .Net, Node.js, SharePoint, client side JS frameworks like Knockout, Angular and React. I am enthusiastic about the learning curve involved in building highly scalable and reliable distributed applications, still learning to apply TDD/DDD.

Other than acquiring/giving fundas at work:-) I love playing badminton and snooker, an aspiring guitarist. I like dancing, but only after a beer is in:-)


This is my personal blog and currently has {{ site.posts | size }} posts in {{ site.categories | size }} categories which combinedly have {{ total_words }} words, which will take an average reader ({{ site.wpm }} WPM) approximately <span class="time">{{ total_readtime }}</span> minutes to read. {% if featuredcount != 0 %}There are <a href="{{ site.url }}/featured">{{ featuredcount }} featured posts</a>, you should definitely check those out.{% endif %}

