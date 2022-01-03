## 5.1. What is Object Oriented Programming? Why Do We Need It?

We come across a lot of different objects in our daily life. Each object has its own properties, some features that define it.

Lets take a ball for example. What are the properties of a ball? Its position, radius, colour and velocity

Now we have previously drawn one ball in p5 and we defined certain variables to keep track of its position and velocity. We did not save its radius or colour in variables. For creating more complicated animations in the future, we'll need to save all of this information as well.

For this purpose, You might try writing code that looks similar to this:

```js
var ball_positionX = 5;
var ball_positionY = 5;

var ball_velocityX = 5;
var ball_velocityY = 5;

var ball_colourR = 255;
var ball_colourG = 0;
var ball_colourB = 0;

var ball_radius = 40

// and then you want a function to update the position of the ball based on its velocity:

function move(posX, posY, velX, velY) {
    return [posX + velX, posY + velY]
}

[ball_positionX, ball_positionY] = move(ball_positonX, ball_positonY, ball_velocityX, ball_velocityY)
```

While, this would work for one ball, but some questions one might have are:

1. What if you wanted to make an unknown number of balls? How would someone know how many variables to declare?
2. What if you had a more complicated object with 100 properties? Would it be feasable to manually declare 100 variables for every object that you might need to create?

This is where classes and object oriented programming come into the picture. You can use classes to define objects that can have properties (like position, colour, velocity, radius) and functions (like move) that operate on and can modify those properties

## 5.2. Classes

Classes are the tool in programming that allow us to create complicated objects effectively using code.

A class is basically a blue-print for creating an object, it tells us the defining properties of the object, and it also tells us what functions the object can perform. Following the class blue-print allows us to create "instances" of that class.

An object of a class, the realisation of the blueprint, is known as an instance of the class.

With this in mind, lets create a ball class in JavaScript that we can use in our p5 sketch!

## 5.3. What makes classes so good?

1. Reusability: The same class can be used to make as many objects as you want
2. Modularity: The code becomes incredibly modular, and it is easy for a programmer to debug the code in case there are any bugs
3. Clarity of code: Due to the code being modular, it is easier for others to read and understand the code
4. Better organisation: The data can be clearly and neatly organised for more complex objects
5. Data Abstraction: This is the process of hiding the implementation details from the user, allowing them to focus on the functionality instead.

    Example: you don't need to know a smartphone works internally to be able to use it. The details about its circuits, its workings are hidden from you, the user! Instead, the smartphone provides you with functions (call, message, surf the internet) only.