---
layout: post
category : JavaScript
title : Block scoping in JavaScript and hoisting
tagline: ""
tags : [JavaScript]
---

Hoisting is the JavaScript interpreter’s action of moving all variable and function declarations to the top of the current scope. This means, the declarations (not the values) will be pushed to top of the current scope before the interpreter starts its job.
For instance, Function declarations are hoisted but the function declarations that are assigned to a variable is not hoisted.

{% highlight javascript %}
foo(); // Function called before initializing

function foo() {
    alert("Hello!");
} // will work
{% endhighlight %}

whereas,

{% highlight javascript %}
foo(); // Function called before initializing
    
var foo = function() {
    alert("Hello!");
}; // will not work
{% endhighlight %}

It get's interesting with ECMAScript 6 with the birth of keyword `let`.
JavaScript is function scoped language, which means   

{% highlight javascript %}
var x = 10;

function temp() {
    var x = 20;
    console.log(x); // Prints 20
}

temp();

console.log(x); // Prints 10  
{% endhighlight %}

Though the value of x is changed to 20 in line 4, line 10 outputs 10. This means, whatever defined inside a fucntion stays inside it and will not affect the global namespace. In function scope, any variables declared within a function are visible anywhere within that same function whereas with block scope, the visibility of variables is confined to any given block (whether it's an if statement, for loop, etc) enclosed by curly braces.

From ECMAScript 6 (JavaScript 1.7), block scoping is possible in JavaScript. `let` is scoped to the nearest enclosing block. For instance,

{% highlight javascript %}
var x = 10; // Globally scoped
let y = "hello"; // Globally scoped

function temp () {
    var x = 10; // Scoped within the function 
    let y = "hello"; // Scoped within the function
}

for ( let x = 0; x < 10; ++x) {
    let x = 10; // Scoped within the block
    var y = "hello"; // Scoped globally
}
// x is not accessible from here but y is accessible here. 
{% endhighlight %}

> Note : The keyword `let` is not hoisted. So, declare them before using it.     

