---
layout: post
title: Simple Jekyll Tags
tags: [jekyll, tips]
---

Jekyll + Github Pages is a streamlined platform for hosting static websites (like this one). Jekyll provides default support for tags, but a little extra work needs to be done to create tag pages. I've read through a lot of great, existing solutions, and I'll try to summarize and simplify them here.

<!--excerpt-->

## Overview

The basic premise is to create a page that includes all posts with a certain tag by iterating through `site.tags` using some Liquid templating logic. We need to make a page for each tag that exists on the site.

Whenever we display a post's tags, we need to give each tag the link to its specific tag page. Again, we can do this quite easily with Liquid.

## Setup

First, we'll have to set up some site data to properly display tag names. You'll likely want to use lowercase names in your posts' front matter and in URL's, but display them to users in a different way.

To do this, we'll leverage Jekyll's `site.data` feature.

If you haven't already, create a `_data/` directory in the root of your website. In that directory, create `tags.yml`, whose contents can be accessed as `site.data.tags`.

In here, we need to create a map between internal tag names (in URL's and front matter) and display tag names.

~~~
jekyll
	name: Jekyll
tips
	name: Tips
~~~

This post has two tags: `jekyll` and `tips`. For each tag, I give it a display name with proper capitalization. You can set the names however you want, but the front matter of the post should use the internal tag. For example, the front matter of this post is

~~~
---
layout: post
title: Simple Jekyll Tags
tags: [jekyll, tips]
---
~~~

To access the name attribute of a given tag called `tag`, we use `site.data.tags[tag].name`.

## Tag Page Layout

The next step is to create a new layout in `_layouts/` for our tag pages. To keep things simple, here is a bare minimum layout page. This file should be named `tag.html`.

{% highlight html %} {% raw %}
---
layout: default
---

<h1>{{ site.data.tags[ page.tag ].name }}</h1>

{% if site.tags[ page.tag ] %}
  {% for post in site.tags[ page.tag ] %}
  <a href="{{ post.url }}">
    <h2>{{ post.title }}</h2>
  </a>
  {% endfor %}
{% else %}
  <p>There are no posts for this tag.</p>
{% endif %}
{% endraw %} {% endhighlight %} 

Using this new layout, we have to create a tag page for every tag you want to use. This is fairly straightforward, but if your site has many tags, a script may speed things up.

For example, the tag page for `jekyll` looks like this:

~~~html
---
layout: tag
tag: jekyll
---
~~~

Name each of these tag pages `tagname.md` and put it a directory called `tag`. This website has a `blog` directory that contains the `tag` directory. Thus, every tag page is accessed by the path `/blog/tag/tagname`.

Depending on how your site is structured, this path may differ.

## Link each tag to its page

Now that a tag page is set up, we have to link the tags in our post to that page. We'll do this with more template logic in the `post` layout.

{% highlight html %} {% raw %}
---
layout: default
---

<h1>{{ page.title }}</h1>

{% if page.tags != empty %}
<ul class="tags">
  {% for tag in page.tags %}
  <li>
    <a href="/blog/tag/{{ tag }}">{{ site.data.tags[tag].name }}</a>
  </li>{% endfor %}
</ul><br>
{% endif %}

<article>
  {{ content }}
</article>
{% endraw %} {% endhighlight %}

The above code adds a list element for every tag included in the page. For the tag link, use the path to wherever you put the tag pages (the example uses `/blog/tag/{% raw %}{{ tag }}{% endraw %}`).

Note that we use the tag's name stored in `site.data.tags` as the display name for the link instead of just the tag itself.

## Summary

Here's a file tree to summarize the additions we made in order to implement tag pages. I've omitted a lot of irrelevant files and folders.

<pre><code>
.
├── index.html
├── _config.yml
├── _data
│   └── <b>tags.yml</b>
├── _layouts
│   ├── default.html
│   ├── <b>post.html</b>
│   └── <b>tag.html</b>
├── _posts
│   └── 2015-08-02-simple-jekyll-tags.md
└── blog
    ├── index.html
    └── <b>tag</b>
        ├── <b>jekyll.md</b>
        └── <b>tips.md</b>
</code></pre>

Now, whenever you click on a 'Jekyll' tag in a post, you get sent to the `jekyll` tag page at `/blog/tag/jekyll`, which displays a list of all posts on the site with the `jekyll` tag.

If you want to add more content to the tag page like dates and read times, check out this site's source on [Github](https://github.com/zhaorz/zhaorz.github.io).
























