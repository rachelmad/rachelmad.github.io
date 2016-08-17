---
layout: large_card
title: "Using Material Design Lite with Jekyll for a simple blog"
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
Head on over to the Material Design Lite site and find a <a href="https://getmdl.io/templates/index.html">template</a> you like. 
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
though, was changing the <code>main</code> section of the document. The <code>main</code> section of mine looks like this:
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

<br>
<p>
You see that I replaced most of it with <code>{% raw %}{{ content }}{% endraw %}</code>. 
This means that the content from all the pages will go into this area. The default layout must be stored as 
<code>default.html</code> in the <code>_layouts</code> directory.
</p>

<h6>3. Create page layouts</h6>
<p>
Page layouts can be thought of as simplified versions of views or components in other frameworks. 
They are reusable templates for the different parts of your site. They must also go as html files into the
 <code>_layouts</code> directory along with your <code>default.html</code>. 
<a href="https://getmdl.io/components/#cards-section">MDL cards</a> are incredibly useful for page layouts. 
I currently only have two layouts, the default and the large card layout. For my blog page,
I loop through all my blog posts and place them inside large cards. 
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
The YAML section, lines 1-3, tells Jekyll which layout this page will use. 
This means that all the code below it will be inserted in the
 <code>{% raw %}{{ content }}{% endraw %}</code> section of the default page.
</p>
<p>
The second part, lines 5-20, loops through all my blog posts. 
Then, <code>{% raw %}{{ post.title }}{% endraw %}</code>, <code>{% raw %}{{ post.tools }}{% endraw %}</code>,
 <code>{% raw %}{{ post.content }}{% endraw %}</code>, and <code>{% raw %}{{ post.display_date }}{% endraw %}</code>
 display the title, tools, content, and date of each post onto different parts of the card.
</p>

<h6>Start writing blog posts!</h6>
<p>
Remember that blog posts need to be titled in this format: <code>YYYY-MM-DD-blog-title</code> and stored in the 
<code>_posts</code> folder. 
The <a href="https://jekyllrb.com/docs/posts/">official site</a> has far better documentation than I will come up with. 
But as a guide, here is my YAML matter for this post:
</p>

{% highlight liquid linenos %}
---
layout: large_card
title: "Using Material Design Lite with Jekyll for a simple blog"
display_date: "August 14, 2016"
tools: Material Design Lite, Jekyll, Github Pages
category: blog
---
{% endhighlight %}

<p>
As I mentioned earlier, <code>layout</code> tells Jekyll which layout to place the blog entry uses. Then, you'll notice
 <code>title</code>, <code>display_date</code>, and <code>tools</code> are the sections I wrote displays for in the previous step. 
 Also, as the name implies, I use <code>category</code> to categorize the files under <code>_post</code>.
  Finally, everything below the YAML matter is considered part of the post's <code>content</code>
</p>
<p>
Later I will go into more detail about how I use categories and how I created the small cards for the projects page. 
But for now, this is all that's needed for a basic blog.
</p>

<p> 
And there you have it! Material Design Lite on Jekyll static pages. 
</p>

