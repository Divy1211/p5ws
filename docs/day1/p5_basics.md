## 2.1. Setup

There are a few different ways to work with p5:

1. Using the [online p5 editor](https://editor.p5js.org/)
2. Making a local p5.js project on your computer. You can code with the IDE of your choice

Some useful plugins for VSC:

1. [p5 Resources](https://marketplace.visualstudio.com/items?itemName=zsakowitz.p5-resources)
2. [p5.vscode](https://marketplace.visualstudio.com/items?itemName=samplavigne.p5-vscode)

## 2.2. Basic Elements of a Sketch

### 1. The Setup Function

The setup function of a p5 sketch is the first function that is run when the sketch is played. Any code that you want to run before your animation begins should go in this function. The most important thing that this function does (usually) is creating the canvas. It is defined like any other function in javascript:

```js
function setup() {
  // run only once code here
}
```

### 2. The Canvas

The canvas is the most basic and important element of any p5 sketch. It is our playing field for drawing all the things that we want to draw to the screen. All p5 sketches have a canvas (even if you don't create one yourself, p5 will create one for you with default 100 x 100 dimensions)

The following setup function creates a canvas of width `400px` and height `200px` and sets a background colour of `RGB(255, 0, 255)` (purple).

```js
function setup() {
    createCanvas(400, 200);
    background(255, 0, 255);
}
```

!!! tip

    If you ever want to access the width and height of your canvas elsewhere in the script, you may think to create your own variables to keep track of them, so that you can easily change them later without having to edit them everywhere in your script. This is extremely good coding practise, and so much so that p5 automatically does this for you! The variables `width` and `height` are special variables defined by p5 itself which, as their names imply, contain the size of the canvas in pixels. Such variables (and functions) that are defined by default by p5 are known as built-ins. You'll see more such variables in the future!


### 3. The Draw Function

The draw function of a p5 sketch is the second most important function that is used to animate the canvas. This function runs 60 times every second and is responsible for updating the canvas. Without the draw function, you can only draw still images with p5

The following code will draw a circle moving across the screen (or does it?):

```js
function setup() {
    createCanvas(400, 400);
    background(200); // a single argument for background specifies the greyscale colour value
}
var centreX = 50;
var dx = 2;
function draw() {
    // draw a circle in each loop
    circle(centreX, 100, 50); // specify the coordinates of the centre of the circle and its radius

    // increment the circle's X coordinate
    centreX+=dx;
}
```

If you just tried that, you probably found out that there was an issue with the animation. The reason is that p5 does not reset the background at each iteration of the draw loop. If you want to do that, you need to do so manually:

```js
function setup() {
    createCanvas(400, 400);
    background(200);
}

var centreX = 50;
var dx = 2;
function draw() {
    // reset the background in each iteration
    background(200);
    circle(centreX, 100, 50);
    centreX+=dx;
}
```

=== "Think"

    Currently the circle goes across the screen and passes through the right edge of the canvas. What if we want to make the circle bounce back when it touches the right edge of the canvas?

=== "Hint 1"

    Currently the circle goes across the screen and passes through the right edge of the canvas. What if we want to make the circle bounce back when it touches the right edge of the canvas?
    
    Hint 1: We know the width of the canvas, and the circle's X coordinate on the canvas. What can you do with this information?

=== "Hint 2"

    Currently the circle goes across the screen and passes through the right edge of the canvas. What if we want to make the circle bounce back when it touches the right edge of the canvas?
    
    Hint 1: We know the width of the canvas, and the circle's X coordinate on the canvas. What can you do with this information?

    Hint 2: Can you use some sort of conditional logic to change the variable `dx` when the circle's X coordinate is outside the width of the canvas?

=== "Solution"

    Currently the circle goes across the screen and passes through the right edge of the canvas. What if we want to make the circle bounce back when it touches the right edge of the canvas?
    
    Hint 1: We know the width of the canvas, and the circle's X coordinate on the canvas. What can you do with this information?

    Hint 2: Can you use some sort of conditional logic to change the variable `dx` when the circle's X coordinate is outside the width of the canvas?
    
    ```js
    function setup() {
        createCanvas(400, 400);
        background(0);
    }

    var centreX = 50;
    var dx = 2;
    function draw() {
        background(200);
        circle(centreX, 100, 50);

        if(width < centreX)
            dx = -2;

        centreX+=dx;
    }
    ```

=== "Bonus Question"

    Currently the circle goes across the screen and passes through the right edge of the canvas. What if we want to make the circle bounce back when it touches the right edge of the canvas?
    
    Hint 1: We know the width of the canvas, and the circle's X coordinate on the canvas. What can you do with this information?

    Hint 2: Can you use some sort of conditional logic to change the variable `dx` when the circle's X coordinate is outside the width of the canvas?

    Bonus: The code for the solution is not perfect, the circle still goes half-way through the edge before it bounces back, and also it still passes through the left edge of the canvas without bouncing. How can we address both of these issues?

=== "Bonus Solution"

    Currently the circle goes across the screen and passes through the right edge of the canvas. What if we want to make the circle bounce back when it touches the right edge of the canvas?
    
    Hint 1: We know the width of the canvas, and the circle's X coordinate on the canvas. What can you do with this information?

    Hint 2: Can you use some sort of conditional logic to change the variable `dx` when the circle's X coordinate is outside the width of the canvas?

    Bonus: The code for the solution is not perfect, the circle still goes half-way through the edge before it bounces back, and also it still passes through the left edge of the canvas without bouncing. How can we address both of these issues?

    ```js
    function setup() {
        createCanvas(400, 400);
        background(0);
    }

    var centreX = 50;
    var dx = 2;
    function draw() {
        background(200);
        circle(centreX, 100, 50);

        if(centreX-25 < 0 || width < centreX+25)
            dx *= -1;

        centreX+=dx;
    }
    ```

## 2.3. p5 Reference

What if you want to draw more shapes than just a circle? There are more functions that you can use to draw shapes in p5, but we need some way to find out the syntax of each function to be able to use them. This is what the [p5 reference](https://p5js.org/reference/) is for. The reference contains the information about each and every p5 built-in function, variable and more.