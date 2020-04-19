---
layout: page
title: by topic
---

## blog archive, by topic

---

## specific areas

Posts on specific research areas or topics.

### \#nonparametricBayes

{% for post in site.posts %}
  {% for tag in post.tags %}
    {% if tag == "nonparametricbayes" %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ site.baseurl }}{{ post.url }})
    {% break %}
    {% endif %}
  {% endfor %}
{% endfor %}

### \#numerics and \#probabilisticnumerics

{% for post in site.posts %}
  {% for tag in post.tags %}
    {% if tag == "numerics" %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ site.baseurl }}{{ post.url }})
    {% break %}
    {% endif %}
  {% endfor %}
{% endfor %}

### \#algorithms

{% for post in site.posts %}
  {% for tag in post.tags %}
    {% if tag == "algorithms" %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ site.baseurl }}{{ post.url }})
    {% break %}
    {% endif %}
  {% endfor %}
{% endfor %}

### \#julia

{% for post in site.posts %}
  {% for tag in post.tags %}
    {% if tag == "julia" %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ site.baseurl }}{{ post.url }})
    {% break %}
    {% endif %}
  {% endfor %}
{% endfor %}
---

## general topics

Posts organized broadly by general topic areas.

### \#statistics and \#machinelearning

{% for post in site.posts %}
  {% for tag in post.tags %}
    {% if tag == "statistics" or tag == "machine learning" %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ site.baseurl }}{{ post.url }})

     {{ post.summary }}...
    {% break %}
    {% endif %}
  {% endfor %}
{% endfor %}

### \#probability

{% for post in site.posts %}
  {% for tag in post.tags %}
    {% if tag == "probability" %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ site.baseurl }}{{ post.url }})

     {{ post.summary }}...
    {% break %}
    {% endif %}
  {% endfor %}
{% endfor %}

### \#computerscience

{% for post in site.posts %}
  {% for tag in post.tags %}
    {% if tag == "computer science" %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ site.baseurl }}{{ post.url }})

     {{ post.summary }}...
    {% break %}
    {% endif %}
  {% endfor %}
{% endfor %}

<!--### \#academics

{% for post in site.posts %}
  {% for tag in post.tags %}
    {% if tag == "academics" %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{site.baseurl }}{{ post.url }})

     {{ post.summary }}...
    {% break %}
    {% endif %}
  {% endfor %}
{% endfor %}
-->

### \#misc

{% for post in site.posts %}
  {% for tag in post.tags %}
    {% if tag == "misc" %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ site.baseurl }}{{ post.url }})

     {{ post.summary }}...
    {% break %}
    {% endif %}
  {% endfor %}
{% endfor %}


