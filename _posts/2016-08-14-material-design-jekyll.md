---
layout: blog_post
title: "Using Material Design Lite with Jekyll for a simple blog"
tools: 
- Material Design Lite
- Jekyll
- Github Pages
category: blog
show: true
comments: true
---

<p>
There are plenty of tutorials out there on setting up Jekyll, but there doesn't seem to be much on styling it. 
So here are the basics of how I am using Jekyll and Material Design Lite for my personal site. 
</p>

<h6>What is Material Design Lite?</h6>
<a href="https://material.google.com/">Material Design</a> is a set of design principles created by Google. 
<a href="https://getmdl.io/index.html">Material Design Lite (MDL)</a> is an easy way to add Material Design aesthetics to your site. 

<h6>1. Get an MDL template</h6>
<p>
Head on over to the Material Design Lite site and find a <a href="https://getmdl.io/templates/index.html">template</a> you like. 
I picked the Portfolio template, as it describes exactly what I wanted to do with my 
<a href="https://pages.github.com/">Github Page</a>: a simple portfolio site to showcase my resume, projects, and even a blog. 
Download the template you like.
</p>

<h6>2. Create Jekyll default layout</h6>
<p>
<a href="https://jekyllrb.com/">Jekyll</a> uses layouts to wrap posts. 
The default layout is used for all pages of the site. 
Any part of your site that should be included in all pages should go to your default page 
<i>(We'll talk about includes later)</i>. 
My default page includes my header, navigation, and footer. 
</p>
<p>
Outside some minor changes, most of my 
<a href="https://github.com/rachelmad/rachelmad.github.io/blob/master/_layouts/default.html">default page</a> looks very similar to the MDL template's index.html page. 
The most important part though, was changing the <code>main</code> section of the document. 
The <code>main</code> section of mine looks like this:
</p>

{% highlight html linenos %}
<main class="mdl-layout__content">
    <div class="mdl-grid portfolio-max-width">
        {% raw  %}
        {{ content }}
        {% endraw  %}
    </div>
</main>
{% endhighlight %}

<p>
You see that I replaced most of it with 
<code>{% raw %}{{ content }}{% endraw %}</code>. 
This means that the content from all the pages will go into this area. 
The default layout must be stored as 
<code>default.html</code> in the 
<code>_layouts</code> directory.
</p>

<h6>3. Create page layouts</h6>
<p>
Page layouts can be thought of as simplified versions of views or components in other frameworks. 
They are reusable templates for the different parts of your site. 
They must also go as html files into the 
<code>_layouts</code> directory along with your 
<code>default.html</code>. 
<a href="https://getmdl.io/components/#cards-section">MDL cards</a> are incredibly useful for page layouts. 
I currently only have two layouts, the default and the large card layout.  
</p>
<p>
Here's a peek of how my 
<a href="https://github.com/rachelmad/rachelmad.github.io/blob/master/_layouts/large_card.html">large card layout</a> looks:
</p>

{% highlight html linenos %}
---
layout: default
---
<div class="mdl-cell mdl-cell--12-col mdl-card mdl-shadow--4dp">
    <div class="mdl-card__title">
        <div class="card-title"> {% raw %}{{ page.card_title }}{% endraw %} </div>
    </div>
    <div class="mdl-grid mdl-card__supporting-text portfolio-copy">
        {% raw %}
        {{ content }}
        {% endraw %}
    </div>
</div>
{% endhighlight %}

<p>
Lines 1-3 are the 
<a href="https://jekyllrb.com/docs/frontmatter/">YAML front matter</a>. 
This tells Jekyll what layout to place the file in. 
Jekyll can contain nested layouts, as in this instance, I am putting the large card layout inside the default. 
Line 4 is the large card container, while lines 5 to 10 display the page's title and content in the appropriate areas. 
The code I used here is based on the MDL template I chose earlier. 
I used the code section for the large card on the 
<a href="https://getmdl.io/templates/portfolio/about.html">About</a> page.
</p>

<h6>4. Use page layouts for various pages</h6>
<p>
The three pages I have using my large card layout are rather similar. 
They only contain a title and a little content. 
Below is the code for my 
<a href="https://github.com/rachelmad/rachelmad.github.io/blob/master/coming-soon.html">coming soon</a> page:
</p>

{% highlight html linenos %}
---
layout: large_card
card_title: "Coming Soon"
---
<div class="mdl-cell mdl-card__supporting-text padding-top">
    <p>
        This page is coming soon! Check back next time!
    </p>
</div>
{% endhighlight %}

<p>
On my YAML matter, I simply indicate the layout the page will use and its title. 
Then below it, I write everything I'd like to appear on the card (which is rather short in this case).
</p>
<p>
I've discussed how I use categories for the experiences, projects, and blog page, 
<a href="/entries/2016/08/27/jekyll-categories">here</a>. 
But for now, this is all that's needed for a basic blog.
</p>

<p> 
And there you have it! Material Design Lite on Jekyll static pages. 
</p>