---
layout: blog_post
title: "Change detection on primitive inputs in Angular 2"
tags: 
- Angular 2
- TypeScript
show: true
---

Detecting input changes in Angular 2 are a bit tricky. 
The way Angular 2 detects changes and handles them can be rather confusing.
Here's how I do it.  

<h6>What are inputs in Angular 2?</h6>
<p>
In Angular 2, parent components can pass data to child components through Inputs. 
On the parent's side, here's a 
<a href="https://github.com/rachelmad/mastermind/blob/master/app/components/pegSet/pegSet.html">sample</a>:
</p>

{% highlight html linenos %}
{% raw %}
<peg [pegColor]="peg1"></peg>
{% endraw %}
{% endhighlight %} 

<p>
In the parent's html, the child component's selector and any inputs are added. 
Inputs are indicated by the square brackets.
</p>

<p>
On the child's side, it looks like <a href="https://github.com/rachelmad/mastermind/blob/master/app/components/peg/peg.ts">this</a>:
</p>

{% highlight javascript linenos %}
{% raw %}
import { Component, Input } from '@angular/core';

@Component({
  selector: "peg",
  templateUrl: 'build/components/peg/peg.html'
})
export class PegComponent {
  @Input() pegColor: string;
  constructor() {}
}
{% endraw %}
{% endhighlight %} 

<p>
Inputs are imported from core and declared using decorators (the @ symbol). 
Any data passed by the parent component to the child can then be accessed using <code>this.user</code>.
</p>

<h6>How does change detection work with Inputs?</h6>
<p>
Angular 2 tracks changes using 
<a href="http://stackoverflow.com/questions/34796901/angular2-change-detection-ngonchanges-not-firing-for-nested-object">dirty checking</a>. 
This means Angular 2 determines that an Input has changed only if the input is primitive. 
So if it's a primitive value like a number, string, or boolean, as soon as the value changes, the child component knows about it.
Moreover, for more complex inputs like arrays, if the reference to the array doesn't change, Angular 2 does not detect it. 
Changes will not be detected for array inputs if only one element in the array was changed. 
</p>

<h6>How to use ngOnChanges for primitive inputs</h6>
<p>
Most likely, the reason you're reading this post is because you want to do something when the input changes. 
This can be done through Angular's <code>ngOnChanges</code> method. 
The documentation for it isn't as detailed as I would have hoped, but here's what I do.
</p>

{% highlight javascript linenos %}
{% raw %}
export class PegComponent implements OnInit, OnChanges {
  @Input() pegColor: string;

  private coloredPeg: boolean;

  ngOnChanges(changes: SimpleChanges) {
    this.pegColorDisplay = changes['pegColor'].currentValue;
    this.coloredPeg = (this.pegColorDisplay !== null);
  }
}
{% endraw %}
{% endhighlight %} 

<p>
The <code>ngOnChanges</code> method is passed a SimpleChanges object when called. 
<code>changes['pegColor'].currentValue</code> accesses the new value of the <code>pegColor</code> input. 
</p>

<p>
And there you have it! I hope this helps!
</p>
