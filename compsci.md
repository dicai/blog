---
layout: page
title: compsci
---

## computer science posts

{% for post in site.posts %}
  {% for tag in post.tags %}
    {% if tag == "computer science" %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }})

     {{ post.summary }}...
    {% break %}
    {% endif %}
  {% endfor %}
{% endfor %}
