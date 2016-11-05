---
layout: blog_post
title: "How to fix mistakes in Git"
tools: Git
category: blog
show: true
---

Git is tricky. 
It gets especially tricky when you've made a mistake and don't know what to do next. 
I've compiled some common mistakes I make and how I remedy them. 

<h6>I staged a file that I shouldn't have</h6>

{% highlight html linenos %}
git reset <filename>
{% endhighlight %} 

<p>
This is probably the easiest because 
<a href="https://git-scm.com">Git</a> 
lists it when you type 
<code>git status</code>, but it's useful to list it down anyway. 
I often end up using it when I have files (like blog drafts) that aren't ready to live in Git yet. 
</p>

<p>
What happens when you 
<code>git add .</code> and your 
<code>.gitignore</code> isn't updated? 
When I accidentally stage 192384738 files that I shouldn't have, I just remove the filename and type 
<code>git reset</code>. 
That unstages all files. 
</p>

<h6>I want to undo my last commit</h6>

{% highlight html linenos %}
git reset --soft HEAD~1 <filename>
{% endhighlight %} 

<p>
Sometimes, I commit and then realize I'd rather add something really quick before committing it (like fixing a lint error that I forgot about). 
This comes in really handy then. 
<a href="https://git-scm.com/docs/git-reset">The command</a> removes the commit but leaves the files in your 
<a href="http://softwareengineering.stackexchange.com/questions/119782/what-does-stage-mean-in-git">staging area</a>. 
Using <code>--soft</code> allows you to keep changes, 
as opposed to <code>--hard</code> which completely discards any changes. 
If you want to undo more than one commit, just think of HEAD~n as n commits before 
<a href="http://stackoverflow.com/questions/2304087/what-is-head-in-git">HEAD</a>. 
So if you want to undo 3 commits, you'd use <code>git reset --soft HEAD~3</code>
</p>

<h6>My last 3 commits basically do the same thing</h6>
<p>
Now this is more of a personal preference. 
But I generally like to keep my git history clean. 
This is an idea I've taken from <a href="http://mislav.net/2013/02/merge-vs-rebase/">Mislav Marohnic</a> 
(you should check out his blog, it's great!). 
</p>

<p>
Ever had one of these?
</p>

{% highlight html linenos %}
Fixed bug
Fixed that bug I thought I fixed
Added something
Fixed that same bug again. Finally.
{% endhighlight %}

I'd prefer that my git log not be littered with commits like that. 
It makes it hard to revert or double check on old code.
Before pushing, I do this instead:

{% highlight html linenos %}
git rebase -i
{% endhighlight %}

<p>
<a href="https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History">The command</a> 
will take you to a revert page where you can choose to edit commit messages, squash commits, or drop them completely. 
I personally end up using squash quite often. 
It's best to do this before doing a push so as not to affect other people, 
but if you're desperate, adding 
<code>HEAD~n</code> to the end allows you modify previous commits even if they've been pushed, just force push afterwards. 
</p>

<h6>I want to delete my last push</h6>

{% highlight html linenos %}
git reset --hard HEAD~1
git push -f
{% endhighlight %}

<p>
This is a bit trickier and definitely shouldn't be used if the repo is shared by multiple people. 
However, for personal projects where I don't have to worry about merge conflicts and diverting branches, I've used it on occasion. 
The <code>-f</code> stands for force. 
<a href="https://git-scm.com/docs/git-push">It</a> 
disable's Git's checks, so use it sparingly. 
</p>

<p>
Sometimes it can take a while Googling to find just the right Git command to use. 
Maybe next time you're in trouble you could just check on this list. 
</p>
