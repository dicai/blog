---
layout: page
title: archive
---

## blog archive

### all posts

{% for post in site.posts %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }})
{% endfor %}

---

## popular tags

### \#statistics and \#machinelearning

{% for post in site.posts %}
  {% for tag in post.tags %}
    {% if tag == "statistics" or tag == "machine learning" %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }})

     {{ post.summary }}...
    {% break %}
    {% endif %}
  {% endfor %}
{% endfor %}

### \#probability

{% for post in site.posts %}
  {% for tag in post.tags %}
    {% if tag == "probability" %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }})

     {{ post.summary }}...
    {% break %}
    {% endif %}
  {% endfor %}
{% endfor %}

### \#computerscience

{% for post in site.posts %}
  {% for tag in post.tags %}
    {% if tag == "computer science" %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }})

     {{ post.summary }}...
    {% break %}
    {% endif %}
  {% endfor %}
{% endfor %}

### \#academics

{% for post in site.posts %}
  {% for tag in post.tags %}
    {% if tag == "academics" %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }})

     {{ post.summary }}...
    {% break %}
    {% endif %}
  {% endfor %}
{% endfor %}

### \#misc

{% for post in site.posts %}
  {% for tag in post.tags %}
    {% if tag == "misc" %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }})

     {{ post.summary }}...
    {% break %}
    {% endif %}
  {% endfor %}
{% endfor %}

---
