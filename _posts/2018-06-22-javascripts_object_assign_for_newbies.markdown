---
layout: post
title:      "JavaScript's Object.assign() for newbies"
date:       2018-06-22 14:04:32 -0400
permalink:  javascripts_object_assign_for_newbies
---


I had my first real introduction to the Object.assign() method while learning how to create pure functions in React to manipulate state.

> A pure function is a function where the return value is only determined by its input values, without observable side effects.
> 

In the world of React this means that we want to create a new state object rather than changing the old state, which we can only accomplish through pure functions.

React reducer functions often make use of the Object.assign() method to return a new state, however the syntax and inner workings are not immediately clear for newbies. 

*disclaimer: user of Object.assign() will likely be overriden by the spread operator syntax proposed for upcomming versions of JS. In the meantime, Object.assign() is still the best way to copy and modify objects*

Here's a breakdown of how Object.assign() works:

**What exactly does Object.assign() do?**

It lets us create a copy of an existing object (the source object) and modify its values, returning a NEW obejct (the target object). Since we are creating a new object, Object.assign() is pure. The original object remains unchanged.

**What is the syntax?**

Object.assign() can take in many paramaters depending on the data that's being copied and modified. The first paramater will be the target object, which is also the return value. If we are creating a new object, the first param would look like this: 
```
Object.assign( {}, )

->  {}
```

The next paramater will be the source object and enumerables which we are copying from. 

```
const obj = {name: "Arya Stark"}
-> {name: "Arya Stark"}

const newObj = Object.assign({}, obj)
-> {name: "Arya Stark"}

obj === newObj
->false
```

From our comparison on the last line of code, we can see that we are in fact creating a new object distinct from the source object.
Our next step is to add our modifications. To add a value or overwrite an existing value from the source object, simply add it in as a param. You can both add and overwrite values in the same param by separating the values with commas.

```
const addValue = Object.assign({}, obj, {kingdom: 'Winterfell'})
-> {name: "Arya Stark", kingdom: "Winterfell"}

const changeValue = Object.assign({}, addValue, {name: 'Ned Stark'})
-> {name: "Ned Stark", kingdom: "Winterfell"}

const addAndChange = Object.assign({}, obj, {name: 'Sansa Stark', kingdom: 'Winterfell'})
-> {name: "Sansa Stark", kingdom: "Winterfell"}
```


There you have it - the easy intro to Object.assign() use. While this method seems straightfoward, it becomes more complex when trying to source from two different objects, or when trying to copy non-enumerable properties. Check out [this blog post](https://medium.com/@tkssharma/objects-in-javascript-object-assign-deep-copy-64106c9aefab) for more in depth info.

