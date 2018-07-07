---
layout: post
title:      "How Hoisting and Scope Work in JavaScript"
date:       2018-07-07 17:19:19 +0000
permalink:  how_hoisting_and_scope_work_in_javascript
---


To truly understand how JavaScript works 'under the hood', you need to understand the concepts of hoisting and scope. Before we can delve into definitions and examples, we first have to learn how JavaScript code is read and executed at run-time. 

JavaScript is an interpreted language, meaning that it does not require a compiler before execution. However, JavaScript has a compilation phase. During the compilation phase, the program hoists variable and function declarations to the top of their scope, but it is not until the execution phase that these variables and functions are defined or executed. Basically, this means that after the compilation phase the program will know about the existance of all declared variables and functions, but will not know their definitions until the exectuion phase. 

# Hoisting

When variable and function declarations are hoisted, the program creates a space for them in memory with a definition of undefined. It is not until the program is executed that the definitions are read.

From a practical standpoint, this means that it doesn't matter where functions and variables are declared, because the declarations will be hoisted to the top of their scope regarless.  It  only matters where they are defined and executed. 

To clarify, let's look at an example. 

```
var hoisted

function test() {
  console.log(hoisted)
  var hoisted = 'defined'
  console.log(hoisted)
}

```

When we run test(), the following is returned: 
```
undefined
defined
=> undefined
```

So what happened here? Why is the first console.log undefined while the second is?
Let's think about what is happening during the compilation phase versus the execution phase. During compilation, the program ran through the entire code block and saw that the variable `hoisted` was declared in the global scope (more on scope in the next section). However, the program does not yet know what `hoisted` is defined as, so when the first console log is hit the program prints 'undefined' (aka what was stored in memory for the variable hoisted during compilation). In the next line we define the variable, which replaces 'undefined' with the string 'defined'. Therefore the second console.log will print 'defined'.

Something weird happens when we declare the variable with **let** or **const** instead of **var**

```
let hoisted

function test() {
  console.log(hoisted)
  let hoisted = 'cool beans'
  console.log(hoisted)
}

test()

=> ReferenceError: hoisted is not defined 
```

What gives?

# Scoping with Var, Let and Const
**var** is the pre ES6 way of declaring variable while **let** and **const** were introduced in ES6. The value of let and const is that they signal whether or not the value will be reassigned - you CAN reassign the value of a variable declared with let, however const cannot be reassigned. This makes code clearer to read and follow along. 

Beyond the reassigning differences, these variables scope differently. Scope is essentially where an element is available within a program. JavaScript has two scops: global and local. The scope of a variable depends on where it is declared; if it is declared outside of a function, it is in the global scope meaning it is available anywhere in the code, and when it is wrapped in a function it will have a local scope, meaning it is only available inside that function.
Since ES6, JS also has block level scoping which constricts a variables scope to a `{}` block, such as in an if or a for statement. 

The introduction of block scoping differentiates how var and let scope - a variable decalred with var will be available outside of the block scope, but a variable declared with let will be confined to the block scope. For this reason it makes sense to use let when looping.

In terms of scope, const behaves like let. The difference between the two is that const cannot be reassigned. Since const cannot be reassigned, it must be initialized at the time of declaration. 

```
// const variable is declared but not assigned

const hoisted

function test() {
    console.log(hoisted)
    const hoisted = 'cool!'
    console.log(hoisted)
}

test()

=> SyntaxError: Unexpected token
//throws an error!
```

however...

```
//does not throw an error, and is in the global scope

const hoisted = 'cool!'

function test() {
    console.log(hoisted)
}

test()
```

Easy enough, so why did our let example above throw a RefferenceError?
When a variable is declared with var, it is assigned a value of undefined during the initialization phase. This is why we will return undefined in the first console.log. 
On the other hand, let and const remain uninitialized during this phase. Since the variable is unitialized, JS will throw an error. 










