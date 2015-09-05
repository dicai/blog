---
layout: page
title: stat-ml
---



## statistics and machine learning posts

### bayesian nonparametrics

{% for post in site.posts %}
  {% for tag in post.tags %}
    {% if tag == "bnp" %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }})

     {{ post.summary }}...
    {% break %}
    {% endif %}
  {% endfor %}
{% endfor %}

### probability

{% for post in site.posts %}
  {% for tag in post.tags %}
    {% if tag == "probability" %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }})

     {{ post.summary }}...
    {% break %}
    {% endif %}
  {% endfor %}
{% endfor %}

### statistical modeling and inference

{% for post in site.posts %}
  {% for tag in post.tags %}
    {% if tag == "inference" or tag == "machine learning" %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }})

     {{ post.summary }}...
    {% break %}
    {% endif %}
  {% endfor %}
{% endfor %}

