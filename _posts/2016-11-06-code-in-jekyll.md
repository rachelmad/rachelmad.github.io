---
layout: blog_post
title: "Displaying code in Jekyll"
tags: 
- Jekyll
- Liquid
- HTML
- CSS
show: true
---

I use Jekyll for this blog and needed to find ways to add code snippets to it. 
It required quite a bit of searching though, 
and the default preferences aren't my favorite. 
Here's how I tweaked mine. 

<h6>Enable Rouge highlighting</h6>
<p>
<a href="https://pages.github.com/versions/">Github pages</a> 
uses <a href="https://jekyllrb.com/">Jekyll</a> 
version 3. 
That means 
<a href="https://sacha.me/articles/jekyll-rouge/">Rouge</a> 
need not be separately installed. 
You can just configure it in the <code>_config.yml</code> 
file by adding or editing the following parameters.
</p>

{% highlight yaml linenos %}
markdown: kramdown
highlighter: rouge
{% endhighlight %} 

<h6>Add syntax CSS to the project</h6>
<p>
Dmitri Moore has created this great 
<a href="https://gist.github.com/demisx/025698a7b5e314a7a4b5">CSS file</a> 
that can be added to the css folder of the project. 
Don't forget to add the following line within the 
<code>head</code> tag of the project.
</p> 

{% highlight html linenos %}
<link href="/css/syntax.css" rel="stylesheet">
{% endhighlight %} 

I also added 
<a href="https://demisx.github.io/jekyll/2014/01/13/improve-code-highlighting-in-jekyll.html">his adjustments</a> 
for better line numbers to the end of the file. 

<h6>Customize the syntax CSS file</h6>
<p>
I wanted to make the code snippets match the rest of my blog. 
So I also added the following minor adjustments: 
</p>

{% highlight css linenos %}
{% raw %}
.highlight {
    background: rgb(230, 230, 230);
    max-height: 300px;
    overflow: scroll;
    border: 1px #C1C1C1;
    border-radius: 3px;
}
{% endraw %}
{% endhighlight %}

<h6>Add code blocks to your posts</h6>
The previous steps allow for code blocks to be written. 
This can be done by adding the following:

{% highlight liquid linenos %}
{% raw %}
{% highlight html linenos %}

	// your code here

{% endhighlight %}
{% endraw %}
{% endhighlight %}

You can change 
<code>html</code> 
to any of the many languages listed 
<a href="https://github.com/jneen/rouge/wiki/List-of-supported-languages-and-lexers">here</a>.

Sometimes, you may have to explain something in Angular or Jekyll itself. 
You don't want Jekyll to interpret the written lines as code. 
The solution is to wrap the code in a raw block

{% assign openTag = '{%' %}

{% highlight liquid linenos %}
{% raw %}
{% raw %}

	// your code here
{% endraw %}
{{ openTag }} endraw %}
{% endhighlight %}

<p>
Side note: 
<a href="http://blog.slaks.net/2013-06-10/jekyll-endraw-in-code/">Schabse Laks</a> 
has a good suggestion on writing the <code>endraw</code> ta itselfg. 
It can get tricky because attempting to use the <code>raw</code> tag on it simply terminates the block and causes an error. 
He uses a liquid variable for the <code>{% raw %}{%{% endraw %}</code> section of the <code>endraw</code> tag. 
</p>

<h6>Add inline code styling</h6>
<p>
In my blog posts, I also occassionally need to add inline code that look like 
<code>this</code>.

For that, I simply use the 
<code>code</code> 
<a href="http://www.w3schools.com/TAgs/tag_code.asp">tag</a>. 

Like the code blocks, I wanted this to match my blog's theme. 
So I also added very similar CSS. 

{% highlight css linenos %}
{% raw %}
code {
    background-color: rgb(230, 230, 230);
    border: 1px solid #C1C1C1;
    border-radius: 3px;
    padding: 2px;
}
{% endraw %}
{% endhighlight %}

<p>
These are the steps I've taken to display readable code on my blog. 
Some of the steps I've taken are based on other people's blogs and discoveries . 
Hope this list is a useful curation of good references on the subject.
</p>

