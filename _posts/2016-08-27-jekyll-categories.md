---
layout: blog_post
title: "Creating a Jekyll portfolio through categories"
tools: Material Design Lite, Jekyll, Github Pages
category: blog
show: true
---

Categories can be added to all Jekyll posts. 
Since I wanted a page that showcased my experience, projects, <i>and</i> blog posts, I use Jekyll to categorize them. 
Here's a rundown of how I use categories and display them in different formats.

<h6>1. Create pages for different sections</h6>
<p>
Recall that various sections of jekyll pages should be placed in their own 
<a href="https://jekyllrb.com/docs/pages/">folders</a>. 
Create these folders and the corresponding <code>index.html</code> pages inside them. 
I have folders named <code>blog</code>, <code>experience</code>, and <code>projects</code>.
</p>

<h6>2. Take note that most things will belong to the <code>_posts</code> folder</h6>
<p>
The word post is typically associated with blog entries (since Jekyll was 
<a href="https://getpocket.com/a/read/2638022">designed for blogs</a>). 
However, since we're adding a little more to it than it's intended purpose, 
the <code>_post</code> folder will basically mean <i>stuff</i>. 
This means that for my case, projects and experiences will be formatted and named as if they're blog posts. 
This is a little of what my 
<a href="https://github.com/rachelmad/rachelmad.github.io/tree/master/_posts">_posts</a> folder looks like.
</p>

{% highlight html linenos %}
_posts
|---2012-01-01-uh.md
|---2015-05-01-fanfiction-checker.md
|---2016-08-14-material-design-jekyll.md
{% endhighlight %} 

<br>
<p>
The first file falls under experiences, and the second, under projects. 
I used dates relatively close to the display dates I wanted as my post name. 
By keeping everything in the <code>_posts</code> folder, 
<a href="https://jekyllrb.com/">Jekyll</a> allows me to loop through them later on.
</p>

<h6>3. Add a category variable to each post file's front matter</h6>
<p>
I added a <a href="https://jekyllrb.com/docs/frontmatter/">category</a> 
(you can also do <code>categories</code> but I'm not a fan of that) on the 
<a href="https://jekyllrb.com/docs/frontmatter/">front matter</a> of each post, categorizing them as either 
<code>experience</code>, <code>project</code>, or <code>blog</code>. 
This will later make it easy for me to sort the posts into the pages they belong to.
</p>

<h6>4. Add any more important variables</h6>
<p>
I am a very big fan of how Jekyll handles front matter. 
I can basically add any variable to it, display it however manner I'd like in my templates. 
This makes it easy to display titles, dates, or tags in a different format. 
Below is how my front matter for projects looks: 
</p>

{% highlight liquid linenos %}
---
layout: large_card
title: "Personal Website"
company: "Independent"
date: "August 2016"
tools: "HTML, CSS, Jekyll, Material Design Lite, Github Pages"
show: true
category: projects
link: https://github.com/rachelmad/rachelmad.github.io
link_name: Github
---
{% endhighlight %}

<p>
I have basic information about the project, like its name and date, link, and the tools I used to create it. 
I also want the ability to easily display and hide projects on my site without manually adding or removing posts.
So I created a boolean value, <code>show</code>, that controls whether or not I want the project to be displayed. 
You can have as many or few values on your YAML matter. 

<h6>4. Create a page for each section</h6>
<p>
The index page for each section will need to loop through all the posts for the particular category. 
This can be done with a simple for loop.
The one on my <a href="https://github.com/rachelmad/rachelmad.github.io/blob/master/projects/index.html">projects index file</a> looks like this: 
</p>

{% highlight html linenos %}
{% raw %}
{% for post in site.categories.projects %}

// Add things here

{% endfor %}
{% endraw %}
{% endhighlight %}

<p>
In my for loop above, I go through all posts in the site that have the category <code>projects</code>. 
Any code that goes inside the for loop is applied to the posts individually. 
</p>
<p>
The first thing I do in my for loop is an <code>if</code> block to check if the <code>show</code> boolean is set to true. 
This makes sure that I'm not displaying projects I don't want to. 
Here's what an <code>if</code> block looks like in Jekyll.
</p>

{% highlight html linenos %}
{% raw %}
{% if post.show == true %}

// Add things here

{% endif %}
{% endraw %}
{% endhighlight %}

<p>
Most of my project card is relatively simple. 
I display the post's title, date, description, and tools, formatting them nicely. 
The most interesting part is the how I handle the link at the bottom. 
Not all projects have a link, so I have 
<code>{% raw %}{% if post.link %}{% endraw %}</code> that executes the block if a link exists. 
Then I have an if-else block that determines if the link is in 
<a href="https://github.com/">Github</a> and should use the <a href="http://fontawesome.io/">Font Awesome</a> Github icon, 
or if it should just display the link name. 
That block looks like this:
</p>

{% highlight html linenos %}
{% raw %}
{% if post.link_name == "Github" %}
    <i class="fa fa-github icon-button fa-2x" aria-hidden="true"></i>
{% else %}
    {{ post.link_name }}
{% endif %}
{% endraw %}
{% endhighlight %}

<p>
And that should be it. Hope someone finds this helpful!
</p>

<p>
If this is interesting, don't forget to check out my entry on 
<a href="/entries/2016/08/14/material-design-jekyll">using material design lite</a> on your Jekyll blog.