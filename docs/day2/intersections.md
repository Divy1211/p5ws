## 6.1. Determining If A Point Is Inside A Given Shape

### 1. Circles

Determining if a point lies inside a circle is simple. We just check the distance of the point from the centre of the circle. If it is greater than the radius of the circle, then the point lies outside the circle. This simple sketch demonstrates this:

```js
let circ = {
    x: 150,
    y: 150,
    r: 100
};
function setup() {
    createCanvas(400, 400);
    background(200);
}
function draw() {
    background(200);
    if(dist(circ.x, circ.y, mouseX, mouseY) <= circ.r)
        fill(255, 0, 0);
    else
        fill(255);
    circle(circ.x, circ.y, 2*circ.r);
}
```

### 2. Rectangles and Squares

Determining if a point lies inside a rectangle (or a square) is also fairly straightforward. If the X and Y coordinates of the point lie between the X and Y coordinates for two opposite corners of the rectangle, then the point lies inside the rectangle. The following sketch demonstrates this:

```js
let rec = {
    x1: 150,
    y1: 100,
    x2: 300,
    y2: 350,
};
function setup() {
    createCanvas(400, 400);
    background(200);
}
function draw() {
    background(200);
    if(rec.x1 < mouseX && mouseX < rec.x2 && rec.y1 < mouseY && mouseY < rec.y2)
        fill(255, 0, 0);
    else
        fill(255);
    rect(rec.x1, rec.y1, rec.x2-rec.x1, rec.y2-rec.y1);
}
```

### 3. Any General Shape

To check if a point lies within any general shape, you draw a line from the point towards the right till the edge of the canvas, and if this line intersects an even number of edges, then the point is outside the shape, otherwise it is inside the shape. The following code demonstrates this:

```js
function setup() {
    createCanvas(400, 400);
    background(200);
}
function pentagon(x, y, edge) {
    let radius = sin(radians(54))/sin(radians(72))*edge;
    let vertices = [];


    beginShape();
    for(i = 0; i < 5; ++i) {
        vertex(x + radius*cos(2*PI*i/5), y + radius*sin(2*PI*i/5));
        vertices.push({x: x + radius*cos(2*PI*i/5), y: y + radius*sin(2*PI*i/5)});
    }
    endShape(CLOSE);
    return vertices;
}
function draw() {
    background(200);

    let vertices = pentagon(100, 100, 50);
    let outside = true;
    let n = vertices.length;

    for(let i = 0; i < n; ++i) {
        let interX = (mouseY-vertices[i].y)*(vertices[i].x-vertices[(i+1)%n].x)/(vertices[i].y-vertices[(i+1)%n].y) + vertices[i].x;
        let minX = Math.min(vertices[i].x, vertices[(i+1)%n].x);
        let maxX = Math.max(vertices[i].x, vertices[(i+1)%n].x);
        let minY = Math.min(vertices[i].y, vertices[(i+1)%n].y);
        let maxY = Math.max(vertices[i].y, vertices[(i+1)%n].y);
        if(mouseX <= interX && minX <= interX && interX <= maxX && minY <= mouseY && mouseY <= maxY)
            outside = !outside;
    }

    if(outside)
        fill(255);
    else
        fill(255, 0, 0);
}
```

## 6.2. Determining If Two Shapes Overlap

### 1. Circles

Determining if two circles overlap is simple. If the distance between their centres is less than the sum of their radii then they overlap.

```js
let circ = {
    x: 150,
    y: 150,
    r: 100
};
let r2 = 50;
function setup() {
    createCanvas(400, 400);
    background(200);
}
function draw() {
    background(200);
    if(dist(circ.x, circ.y, mouseX, mouseY) <= circ.r+r2)
        fill(255, 0, 0);
    else
        fill(255);

    circle(circ.x, circ.y, 2*circ.r);
    circle(mouseX, mouseY, 2*r2);
}
```

### 2. Rectangles

Determining if two rectangles overlap is also fairly simple. If the manhattan distance between their centres is less than half the sum of their length and widths.

```js
let rec = {
    x: 150,
    y: 100,
    w: 100,
    h: 50,
};
let rec2 = {
    w: 50,
    h: 100,
};

function setup() {
    createCanvas(400, 400);
    background(200);
}

function mdist(x1, y1, x2, y2) {
    return Math.abs(x2-x1) + Math.abs(y2-y1);
}

function draw() {
    background(200);
    if(Math.abs(mouseX-rec.x) < (rec.w+rec2.w)/2 && Math.abs(mouseY-rec.y) < (rec.h+rec2.h)/2)
        fill(255, 0, 0);
    else
        fill(255);
    rect(rec.x-rec.w/2, rec.y-rec.h/2, rec.w, rec.h);
    rect(mouseX-rec2.w/2, mouseY-rec2.h/2, rec2.w, rec2.h);
} 
```