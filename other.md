---
layout: page
title: other topics
---

## other posts

<!--
### academics

{% for post in site.posts %}
  {% for tag in post.tags %}
    {% if tag == "academics" %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ site.baseurl }}{{ post.url }})

     {{ post.summary }}...
    {% break %}
    {% endif %}
  {% endfor %}
{% endfor %}
-->

### miscellaneous

{% for post in site.posts %}
  {% for tag in post.tags %}
    {% if tag == "misc" %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ site.baseurl }}{{ post.url }})

     {{ post.summary }}...
    {% break %}
    {% endif %}
  {% endfor %}
{% endfor %}

