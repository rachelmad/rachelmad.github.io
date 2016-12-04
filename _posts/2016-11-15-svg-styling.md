---
layout: blog_post
title: "Changing SVG styles with the DOM API"
tags: 
- SVG
- JavaScript
- CSS
category: blog
show: true
---

SVGs are great. 
Not only do they render non-pixelated versions of your favorite vector images, 
but their XML base allows developers so much freedom to play with them. 
It's also a good exploration of what can be done with the DOM API. 

<h6>Accessing the SVG</h6>
<p>
It turns out that the  
<a href="https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model">DOM API</a> can be used not only for HTML, 
but XML and SVG as well. 
SVGs can then be accessed by any DOM API method you choose. 
The simplest and most common one is through the 
<code>getElementById</code> 
<a href="https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementById">method</a>.
</p>

{% highlight javascript linenos %}
let svg = document.getElementById("my_svg");
{% endhighlight %}

<p>
SVGs inside <code>object</code> tags or iframes need an additional step. 
After getting the object or iframe element, 
you'll need to use <code>contentDocument</code> to access its SVG content. 
</p>

{% highlight javascript linenos %}
let obj = document.getElementById("objectsvg");
let svgdoc = obj.contentDocument;
let svg = svgdoc.getElementById("my_svg");
{% endhighlight %}

<p>
Note that if an SVG is displayed using an 
<code>img</code> tag, 
the following steps won't work.  
<code>img</code> tags render the SVGs as just that, images. 
Thus, their DOM elements can no longer be accessed programmatically. 
</p>

<h6>Accessing child elements</h6>
<p>
Elements within the SVG are inside the <code>children</code> attribute. 
It is in the form of an 
<a href="https://developer.mozilla.org/en-US/docs/Web/API/HTMLCollection">HTMLCollection</a> though.
Since HTMLCollections aren't 
<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_Generators">iterators</a> 
they can't be looped through using a <code>forEach</code>. 
It needs to be iterated using the classic, 
<code>{% raw %}for (let i = 0; i < svg.children.length; i++){% endraw %}</code>

<h6>Changing style</h6>
<p>
SVG element styles can easily be changed. 
Each element has a <code>classList</code>, 
as its name implies, it's a collection of an element's classes. 
This attribute is read-only though and can only be manipulated through its <code>add</code> and <code>remove</code> 
<a href="https://developer.mozilla.org/en-US/docs/Web/API/Element/classList">methods</a>.  
Below is a sample of iterating through elements in an SVG, 
changing all of one class into another.
</p>

{% highlight javascript linenos %}
for (let i = 0; i < svg.children.length; i++) {
    let child = svg.children[i];
    if (child.classList.contains("oldstyle")) {
        child.classList.remove("oldstyle");
        child.classList.add("newstyle");
    }
}
{% endhighlight %}


