---
layout: blog_post
title: "Creating a Jekyll portfolio through categories"
tags: 
- Material Design Lite
- Jekyll
- Github Pages
show: false
---

Over time, I've learned that Git is something that everyone assumes that everyone else knows. 
It seems that that's not really the case though.
I've listed some of my favorite Git commands, 
from the simple ones you learn on day one, to some cooler ones I've picked up over time.

<h6>Basic commands</h6> 
{% highlight html linenos %}
git add path/to/file
git commit -m "Your commit message"
git push
{% endhighlight %}

<h6>Creating a new repository</h6>
{% highlight html linenos %}
git init
{% endhighlight %}

<h6>Cleaning up commits</h6>
<p>
I mostly only commit at good stopping points. 
This means that I only do so when I know pushing will not break anything.
This makes it easy to clean up commits before pushing as well. 
Ever had one of these?

{% highlight html linenos %}
Changed fixed bug
Fixed that bug I thought I fixed
Added something
Fixed that same bug again. Finally.
{% endhighlight %}

I'd prefer that my git log not be littered with commits like that. 
It makes it hard to revert or double check on old code.
Before pushing, I do this instead:

{% highlight html linenos %}
git revert -i
{% endhighlight %}

<p>
Did I miss anything? 
Are there more efficient ways to do the things I've listed? 
Let me know!
</p>