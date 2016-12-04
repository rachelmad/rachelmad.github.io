---
layout: blog_post
title: "JavaScript Basics"
tags: 
- JavaScript
category: blog
show: true
---

Lately whenever I've had some idle time, 
whether that be waiting for my Windows box to start up, 
or waiting for my project to build, 
I've been reading MDN's JavaScript docs. 
As someone who's never formally studied JavaScript, 
it has plenty of useful tidbits that I may not gather from just building applications. 

<h6><code>null</code> and <code>undefined</code> are considered data types in JavaScript</h6>

<p>
This probably comes in more useful for random trivia and interviews than anything else. 
But unlike Java, where 
<code>null</code> is simply a possible value, 
<code>null</code> is one of 
<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_Types#Data_structures_and_types">6 primitive data types in JavaScript</a> 
(Boolean, null, undefined, Number, String, and Symbol).
</p>

<h6>Don't use <code>for ... in</code> to loop through arrays</h6>
<p>
<code>for ... in</code> loops through an object's 
<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Loops_and_iteration#for...in_statement">property values</a>, 
not array values. 
So if you have an array with extra user-defined properties, 
looping using 
<code>for ... in</code> would list all its existing elements 
<i>and</i> the user-defined properties. 
For arrays, it's better to use 
<code>for ... of</code>. 
Luckily, I've never run into this issue. 
I always use the other alternative, <code>forEach</code>.

<h6>Primitive parameters are passed by value, non-primitive values are passed by reference</h6>
<p>
I had already figured this out through experience, 
but it's always nice to have confirmation. 
This is unlike C++, where you get to choose the manner a variable is passed.
</p>

<h6>Rest parameters</h6>
<p>
Rest parameters allow the representation of an 
<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions#Rest_parameters">indefinite number of arguments</a> 
as an array. 
I have never had to use this in JavaScript, 
but it does remind of a similar idea in Java, 
<a href="https://docs.oracle.com/javase/1.5.0/docs/guide/language/varargs.html">varargs</a>. 
I'm pretty excited to find a need for this concept in my projects. 
</p>

<h6>Anonymous functions</h6>
<p>
Learning TypeScript and ES2016 before anything else, 
I have never had the need to use the long hand for 
<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions#Arrow_functions">anonymous functions</a>. 
Instead, I always just use fat arrows. 
But reviewing its syntax is always helpful, 
especially for reading other people's code. 
</p>

<h6>Maps</h6>
<p>
As a Python lover, I used 
<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Keyed_collections#Map_object">maps</a> 
heavily when I first started using JavaScript. 
However, I only learned in the documentation that 
map keys don't need to be strings, 
and map iteration occurs in the order of insertion. 
</p>

<h6>Sets</h6>
<p>
I, unfortunately, was not aware of the existence of 
<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Keyed_collections#Set_object">Sets</a>. 
They can be compared to Arrays, but only contain unique values. 
And for cases where relevant, it may be better to use them because 
they can check element existence faster, 
delete objects by value (instead of index), 
and can store NaNs. 
</p>

<p>
Note: I was also not aware that Arrays can't store NaNs properly.
</p>
