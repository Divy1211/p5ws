## 3.1. Activity (10 Minutes)

Using google search or the [p5 reference](https://p5js.org/reference/), find out how to do the following:

1. Draw a rectangle
2. Draw a point
3. Draw a line joining two points
4. Draw a square
5. Draw a triangle
6. Draw an ellipse

## 3.2. Stroke and Fill Options

To change the colour of the outline (stroke) of a shape, we can use the `stroke()` function. As you may guess, this function accepts an RGB or Greyscale value as an input:

`stroke(255);` changes the stroke to white.

`stroke(255, 255, 0);` changes the stroke to yellow.

Additionally, you can also specify an alpha value along with the RGB or Greyscale values:

`stroke(255, 127);` changes the stroke to a half transparent white.

`stroke(255, 255, 0, 255);` changes the stroke to a fully opaque yellow.

If you don't want to have an outline at all, you can use `noStroke();`

To change the colour of the fill of a shape, we can use the `fill()` function. Its arguments work exactly the same as the stroke function. If you don't want to have a fill for your shape, you can use `noFill();`

Note that these functions must be called BEFORE you draw the shapes for which you want them to apply. Also note that once the stroke is changed, it will remain that way until changed again.

There are many more functions that can change the way that shapes are drawn, you do not need to memorise all of their syntaxes, but just need to know how to look them up in the reference (or even search on google) for them when you need to use them. As an exercise, can you find the function that changes the thickness of the outline of shapes in the reference?

## 3.3. Custom Shapes

What if you want to make a shape that does not have a built-in function in p5? For this purpose, p5 lets us define custom shapes very simply using three functions called `beginShape()`, `vertex()`, `endShape()`

Lets say that you want to create pentagons. The following function can be used to do so:

```js
function pentagon(x, y, edge) {
    let radius = sin(radians(54))/sin(radians(72))*edge;
    beginShape()
    for(i = 0; i < 5; ++i)
        vertex(x + radius*cos(2*PI*i/5), y + radius*sin(2*PI*i/5))
    endShape()
}
```

Now you may notice, that one of the edges of the pentagon is missing. This is because the shape is not closed by default. The missing edge is the one that should be drawn between the first vertex and the last vertex. To make the shape closed, we can pass in the constant `CLOSE` as an argument to the `endShape` function.

```js
function pentagon(x, y, edge) {
    let radius = sin(radians(54))/sin(radians(72))*edge;
    
    beginShape()
    for(i = 0; i < 5; ++i)
        vertex(x + radius*cos(2*PI*i/5), y + radius*sin(2*PI*i/5))
    endShape(CLOSE)
}
```

## 3.4. Transformations

Now you might also notice that the pentagon is not "flat". It is currently slightly rotated. This issue can be fixed by using an anti clock wise rotation.

```js
function pentagon(x, y, edge) {
    let radius = sin(radians(54))/sin(radians(72))*edge;
    
    rotate(radians(-18));

    beginShape()
    for(i = 0; i < 5; ++i)
        vertex(x + radius*cos(2*PI*i/5), y + radius*sin(2*PI*i/5))
    endShape(CLOSE)
}
```

Now you may note that after doing the rotation, the pentagon is no longer correctly centred. The reason for this is that the rotation happens around the origin of the canvas (which is at the top left). This means that anything drawn at a given (x, y) is first rotated anti clockwise by 18 degrees around (0, 0) before being displayed on the canvas.

For the pentagon to be centred correctly, we need to rotate about the centre of the pentagon, and not the origin. For this, we can make use of the `translate()` function. This function moves the origin to the specified coordinates (x, y)

```js
function pentagon(x, y, edge) {
    let radius = sin(radians(54))/sin(radians(72))*edge;

    translate(x, y);
    rotate(radians(-18));

    beginShape()
    for(i = 0; i < 5; ++i)
        vertex(radius*cos(2*PI*i/5), radius*sin(2*PI*i/5))
    endShape(CLOSE)
}
```

You may have also noticed that if you now try to make another shape, its rotation is not correct either! The reason for this is that just like `stroke()`, changes made by functions like `rotate()` and `translate()` are also settings that need to be changed manually. More formally, these rotations and translations are known as linear transformations. To fix our shape situation, one option is to reverse all the transformations that we make.

```js
function pentagon(x, y, edge) {
    let radius = sin(radians(54))/sin(radians(72))*edge;

    translate(x, y);
    rotate(radians(-18));

    beginShape()
    for(i = 0; i < 5; ++i)
        vertex(radius*cos(2*PI*i/5), radius*sin(2*PI*i/5))
    endShape(CLOSE)

    rotate(radians(18));
    translate(-x, -y);
}
```

While this works, this is not very manage-able in the long run if you make hundreds or thousands of transformations in your sketch, you simply can't keep track of them all to reverse them. Even if you could keep track, it would take time and computational power to reverse them. Due to these reasons, p5 offers us a way to save the current transformation settings by using `push()` function. They can then be restored by using the `pop` function.

```js
function pentagon(x, y, edge) {
    let radius = sin(radians(54))/sin(radians(72))*edge;

    push();

    translate(x, y);
    rotate(radians(-18));

    beginShape()
    for(i = 0; i < 5; ++i)
        vertex(radius*cos(2*PI*i/5), radius*sin(2*PI*i/5))
    endShape(CLOSE)

    pop();
}
```

Note: while `push()` and `pop()` are mainly used to save and restore transformation settings, they also save and restore ANY other settings for the canvas like stroke and fill.