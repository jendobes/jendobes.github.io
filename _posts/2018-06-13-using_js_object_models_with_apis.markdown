---
layout: post
title:      "Using JS Object Models with APIs"
date:       2018-06-13 23:08:38 +0000
permalink:  using_js_object_models_with_apis
---


After working with an object oriented language like Ruby, the transition to procedural programming can be tough. Luckily in JavaScript, there are prototyping methods that give familiar OOP functionality. I found these methods to be confusing at first, so here is an intro guide to prototyping in Javascript. 

The [Mozilla docs ](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Details_of_the_Object_Model) tell us that instead of using classes and instances to create objects, we instead create prototypes from which objects are made. What does this actually mean? When you create a prototype, you are esentially adding new, custom functionality to the Object model. This new prototype will have all the functionality of any Object in JS, along with whatever attributes and methods we give it. Any new object we create off this prototype (using the new constructor, more info below) will inherit our added functionality. 

Lets look at an example. Say we want to create a Pet object which has a name, breed and age. In ruby we would do something like this:

```
class Pet
  attr_accessor :name, :breed, :age
	
	def initialize(name, age, breed)
	@name = name
	@age = age
	@breed = breed
	end
	
end
```

In JavaScript, instead of creating a class, we build a function. Per convention, the function name will be uppercase to indicate that it is an Object constructor. This constructor function will create new objects based on the passed in data. 

```
function Pet(name, age, breed) {
this.name = name,
this.age = age,
this.breed = breed
}
```

Easy!

In ruby, we create a new instance of the pet class with the 'new' operator, per the below:

```
nala_cat = Pet.new('Nala', 4, 'Long Hair Domestic')
```

Javascript also makes use of a 'new' operator, however it is important to note that we are not creating an instance here. We are just creating an object off of the Pet.prototype, which is also an object.

```
let nalaCat = new Pet('Nala', 4, 'Long Hair Domestic')
```

Now when we type nalaCat into the console, we should see an object with attributes!

```
Pet {name: "Nala", age: 4, breed: "cat"}
```

This pattern becomes extemely useful when working with APIs in JS. Creating Object Models allows us to take data returned in json and transform it into objects that are really natural to work with. We can pretend we're using Object Oriented Programming!

Let's say I got a bunch of pet data from a shelter's API, and I wanted to creat a Pet object for each animal (ideal for templating and accessing data down the line).
A simple way to do this would be to create a forEach() loop that passes each pet data array to my Pet prototype to create my objects. Say I still want to track the name, age and breed of each pet (and each of those attributes are included in the returned API data). I would modify my Pet model function to find the data I want and assign it to the corresponding object attributes: 

```
function Pet(petData) {
this.name = petData.name,
this.age = petData.age,
this.breed = petData.breed
}
```

My forEach loop would look like so:

```
function(jsonData) {
jsonData.forEach(petData => {
  let pet = new Pet(petData)
  }
}
```

Voila! We can now work with json data and APIs using OOP methods. 

