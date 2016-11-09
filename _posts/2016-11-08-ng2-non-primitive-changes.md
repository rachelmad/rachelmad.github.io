---
layout: blog_post
title: "Non-Primitive Inputs in Angular 2"
tools: Angular2, TypeScript
category: blog
show: true
---

Remember when I talked about how Inputs in Angular 2 can be tricky? 
Well it gets worse. 
Here are some points to keep in mind when passing non-primitive types as Inputs.

<h6>ngOnChange won't work</h6>
<p>
As <a href="/entries/2016/11/02/primitive-input-changes">I've mentioned before</a>, 
<a href="https://angular.io/">Angular 2</a> 
uses dirty checking. 
This means that for non-primitive data types, 
it can only tell a change has occurred if the Input's memory address has changed. 
Thus, the 
<a href="https://angular.io/docs/ts/latest/api/core/index/OnChanges-class.html">ngOnChanges</a> 
method will not be called. 
</p>

<h6>Changes in the child component are reflected in the parent</h6>
<p>
Take this as an example:
</p>

{% highlight typescript linenos %}
{% raw %}
export class Parent {
	private sample = {
		"text": "original"
	};
}
{% endraw %}
{% endhighlight %}

{% highlight html linenos %}
{% raw %}
<parent>
	<child [sampleInput]="sample"></child>
	{{ sample.text }}
</parent>
{% endraw %}
{% endhighlight %}

{% highlight typescript linenos %}
{% raw %}
export class Child {
	@Input() sampleInput;
	
	changeSample() {
		this.sampleInput.text = "changed";
	}
}
{% endraw %}
{% endhighlight %}

<p>
The idea, in words, is pretty simple, 
The sample object passed from the parent to the child can be changed by the 
<code>changeSample</code> method. 
And by changing the 
<code>sampleInput</code> object in the 
<code>Child</code> class, the changes are immediately seen on the sample object in the 
<code>Parent</code> class. 
</p>

<p>
However, words and application are a completely different thing. 
I spent a good chunk of my afternoon earlier debugging, 
trying to identify why an object in a particular class had its data changed when it shouldn't have been. 
It took a while to conclude that it was because the object was passed onto another class, 
and it took even longer to find which particular class was changing it. 
</p>


