---
layout: large_card
title: "How to use Material Design Lite with Jekyll"
display_date: "August 14, 2016"
tools: Material Design Lite, Jekyll, Github Pages
category: blog
---

<p>
There are plenty of tutorials out there on setting up Github Pages with Jekyll, 
but there doesn't seem to be much on styling it. So here's a quick run down on how I 
am using Github Pages, Jekyll, and Material Design Lite for my personal site. 
</p>

<h6>What is Material Design Lite?</h6>
<a href="https://material.google.com/">Material Design</a> is a set of design principles created by Google. 
<a href="https://getmdl.io/index.html">Material Design Lite (MDL)</a> is an easy way to add Material Design aesthetics to your site. 

<h6>1. Get an MDL template</h6>
<p>
Head on over to <a href="https://getmdl.io/templates/index.html">the Material Design Lite site</a> and find a template you like. 
I picked the Portfolio template, as it describes exactly what I wanted to do with my 
<a href="https://pages.github.com/">Github Page</a>: a simple portfolio site to showcase
my resume, projects, and even a blog. Download the template you like.
</p>

<h6>2. Create Jekyll default layout</h6>
<p>
<a href="https://jekyllrb.com/">Jekyll</a> uses layouts to wrap posts. The default layout is used for all pages of the site. 
Any part of your site that should be included in all pages should go to your default page <i>(We'll talk about includes later)</i>.
 My default page includes my header, navigation, and footer. 
</p>
<p>
Outside some minor changes, most of my 
<a href="https://github.com/rachelmad/rachelmad.github.io/blob/master/_layouts/default.html">default page</a>
 looks very similar to the MDL template's index.html page. The most important part
though, was changing the <code>main</code> section of the document. A simplified version of mine looks like this:
</p>

{% highlight html linenos %}
<html lang="en">
<head>
</head>
<body>
<div class="mdl-layout mdl-js-layout mdl-layout--fixed-header">
    <header class="mdl-layout__header mdl-layout--fixed-header portfolio-header">
    </header>
    <div class="mdl-layout__drawer">
        <nav class="mdl-navigation mdl-typography--body-1-force-preferred-font">
        </nav>
    </div>
    <main class="mdl-layout__content">
        <div class="mdl-grid portfolio-max-width">
            {% raw  %}
            {{ content }}
            {% endraw  %}
        </div>
    </main>
    <footer class="mdl-mini-footer">
    </footer>
</div>
<script src="https://code.getmdl.io/1.1.3/material.min.js"></script>
</body>
</html>
{% endhighlight %}

<br>
<p>
On line 15, you see that I replaced most of the <code>main</code> section with {% raw %} {{ content }} {% endraw %}. 
This means that the content from all the pages will go into this area. 
</p>
<p>
This file can be reduced further once we add <a href="http://jekyll.tips/jekyll-casts/includes/">includes</a>.
 But for now, I'll leave it like this.
</p>

<h6>3. Create page layouts</h6>
<p>
<a href="https://getmdl.io/components/#cards-section">MDL cards</a> are incredibly useful for page layouts. 
I used two main patterns for my pages, large cards and small cards. For my blog page,
I loop through all my blog posts and place them inside large cards. Then for my projects page, I loop through all my projects and 
put them in small cards. I don't even have to worry about card placements or grids. MDL has that all covered.
</p>
<p>
Here's a peek of how my <a href="https://github.com/rachelmad/rachelmad.github.io/blob/master/blog/index.html">blog index page</a>
 looks:
</p>

{% highlight html linenos %}
---
layout: default
---

{% raw %}{% for post in site.categories.blog %}{% endraw %}
<div class="mdl-cell mdl-cell--12-col mdl-card mdl-shadow--4dp">
    <div class="mdl-card__title">
        <div class="card-title"> {% raw %}{{ post.title }}{% endraw %} </div>
    </div>
    <div class="mdl-grid mdl-card__supporting-text">
        <div class="subtext"><span class="keywords"> {% raw %}{{ post.tools }}{% endraw %} </span></div>
        <div class="portfolio-description">
            {% raw %}{{ post.content }}{% endraw %}
        </div>
        <div class="subtext">
            {% raw %}{{ post.display_date }}{% endraw %}
        </div>
    </div>
</div>
{% raw %}{% endfor %}{% endraw %}
{% endhighlight %}

<br>
<p>
And there you have it! Material Design Lite on Jekyll static pages. 


