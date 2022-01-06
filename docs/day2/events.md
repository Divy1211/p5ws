## 4.1. What are Events?

Lets say that you want to change the background of the canvas to a random colour everytime someone left clicks. How would you go about doing this? This is where events come in. Events are special actions or occurances that are recognised by the software/framework/library that you're working with. With every event, there is a corresponding function that is called when that event occurs.

## 4.2. Detecting and Identifying Mouse Clicks

When you click with your mouse, the `mousePressed()` function is called, the built-in boolean variable `mouseIsPressed` is set to `true` and the variable `mouseButton` is set to whatever button was pressed on the mouse. It can be one of three different values, `LEFT`, `RIGHT`, or `MIDDLE`

This is how we can use this function to set the background to a random colour everytime someone left clicks:

```js
function mousePressed() {
    if(mouseButton === LEFT) {
        var r = random(256);
        var g = random(256);
        var b = random(256);

        background(r, g, b);
    }
}
```

There are similar functions and variables for events related to keyboard and touch input. You can find out more about them by looking through the reference!