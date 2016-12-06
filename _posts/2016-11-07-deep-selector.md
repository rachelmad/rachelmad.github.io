---
layout: blog_post
title: "Angular 2's deep selector"
tags: 
- Angular 2
- Ionic 2
- CSS
show: true
---

What if I want to change the styles of child components in Angular 2?
Is that even possible?
Well, yes. 

<p>
<a href="https://angular.io/">Angular 2's</a> 
<a href="https://angular.io/docs/ts/latest/guide/component-styles.html">deep selector</a> 
allows a parent component to alter its children's CSS. 
</p>

{% highlight html linenos %}
<parent>
	<child></child>
	<child2></child2>
	<child3></child3>
</parent>
{% endhighlight %}

{% highlight css linenos %}
/deep/ .padding {
	padding: 15px;
}
{% endhighlight %}

<p>
If I add the CSS snippet above to the <code>parent</code> component, 
I can change all elements with the class 
<code>padding</code> in the three child components.
</p>

<p>
This becomes useful when you need to alter the CSS of a component you can't edit. 
In my case, I had to change the colors of a component in a library that I had imported through NPM.
It would be irrational to dig into the <code>node_modules</code> folder and change the CSS of the component itself. 
I had to find a way to alter the library through my own code. 
</p>
  
<p>
It's important to note that this selector can only be used with emulated view encapsulation. 
Unfortunately, view encapsulation is 
<a href="https://github.com/driftyco/ionic/issues/7206">turned off in Ionic 2</a>.
So the deep selector cannot be used for now. 
</p>
 
