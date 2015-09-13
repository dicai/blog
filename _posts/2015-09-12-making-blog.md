---
layout: post
title: Making this blog with Jekyll, Hyde, MathJax, ...
tags:
- misc
summary: I recently switched my old Wordpress.com blog over to using Jekyll. The main reasons were due to better math display and easier $$\LaTeX$$ parsing but also because it was easier to customize the layout.
---

I recently switched my old Wordpress.com blog over to using Jekyll. The main reasons were
due to better math display and easier $$\LaTeX$$ parsing but also because it was
easier to customize the layout (making the layout uses HTML, CSS, Liquid
        templating code, and posts are written in Markdown).

I used [Hyde](https://github.com/poole/hyde), which is a Jekyll (a static website generator) theme based on Poole. To get this set up, fork
the repository and follow the instructions for the Hyde and
[Poole](https://github.com/poole/poole) READMEs
(basically, you install Ruby and Jekyll).

I changed the content to fit my website in `_config.yml` -- essentially the
sidebar text. Then to build the site:

{% highlight bash %}
jekyll build
{% endhighlight %}

To run the project locally:

{% highlight bash %}
jekyll serve
{% endhighlight %}

I then copied over my blog posts into the `_posts` directory, where each post was
prefaced by (the YAML frontmatter)

~~~
---
layout: post
title: blah
summary: blah blah blah
---
~~~

and then I made some changes to put things like headings in Markdown (see
[this page](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) for a great Markdown cheatsheet).

Unfortunately, the math rendering was a mess, so I had to make a few changes to
fix this.

### MathJax

Then I added MathJax -- basically this meant including MathJax on the
`_includes/head.html` page and a few other tweaks. In `head.html`, I included the block:

{% highlight html %}
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
{% endhighlight %}

in the head of the file.

Previously, the syntax for entering LaTeX inline was "$latex 2+2$," whereas
now I can type "\\\\( 2+2 \\\\)$" (or define my own macros) and "\\\\[ 2+2 \\\\]"
for block math rendering.

To get MathJax to play nice, I modified the `_config.yml` to use `kramdown` for
the markdown (see [this post](https://gist.github.com/mikelove/cbf6eb431406852ba725).)
For more details, see this [blog post](http://christopherpoole.github.io/using-mathjax-on-github-pages/).
With a few find and replaces in vim, I changed the old syntax to the new syntax
pretty easily (kramdown recognizes $$ syntax).

<b>Note</b>: upon writing this blog post, I realized using kramdown in Jekyll has
issues with syntax highlighting. A fix is to put [this repo](https://github.com/mvdbos/kramdown-with-pygments)
in a folder called `_plugins` and then edit the `_config.yml` file
to use `KramdownPyments` for the markdown.
Also note that [code blocks](http://kramdown.gettalong.org/syntax.html#code-blocks)
are also different than traditional markdown.
A nice alternative to using a plugin to do this
is to use Liquid highlighting, where you include code inside the tags:

{% highlight liquid %}
{% raw %}
{% highlight python %}
    print('hello world!')
{% endhighlight %}
{% endraw %}
{% endhighlight %}

### Adding tags

My old blog had tabs corresponding to a few tags. I wanted to recreate that in
the sidebar. I mostly followed [this blog post](http://charliepark.org/tags-in-jekyll/).

First I added tags I wanted in the frontmatter of each post:

~~~
tags:
- machine learning
- statistics
~~~

Now to add things to the sidebar, I created a few files in the top level
directory: `archive.md`, `statml.md`, `compsci.md`, and `other.md`.
Each file looked something like this:

~~~
---
layout: page
title: compsci
---

## computer science posts
{% raw %}
{% for post in site.posts %}
  {% for tag in post.tags %}
    {% if tag == "computer science" %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ site.baseurl }}{{ post.url }})

     {{ post.summary }}...
    {% break %}
    {% endif %}
  {% endfor %}
{% endfor %}
{% endraw %}
~~~

This is basically a modification of [this blog post](http://joshualande.com/jekyll-github-pages-poole/) but looping over the tags as well.
Here `site.baseurl` is set in `_config.yml`.

I also modified `_layouts/page.html` to get rid of displaying post.title at the
top.


### Other tweaks

I added Twitter widgets to each post by putting in `_layouts/post.html` the block:

{% highlight html %}
<a href="https://twitter.com/share" class="twitter-share-button"
data-via="d1ca1">Tweet</a>

<script>!function(d,s,id){var js,fjs=d.getElementsByTagName(s)[0];if(!d.getElementById(id)){js=d.createElement(s);js.id=id;js.src="//platform.twitter.com/widgets.js";fjs.parentNode.insertBefore(js,fjs);}}(document,"script","twitter-wjs");</script>
{% endhighlight %}

To add font awesome icons, add this line in `_includes/head.html`.

{% highlight html %}
<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css">
{% endhighlight %}

