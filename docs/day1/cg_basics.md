## 1.1. Pixels

A pixel, or picture element, is the smallest part of a screen or image that can light up independently from any other part of the screen. Each screen or image has a resolution, i.e. the number of pixels that is has in each direction. For instance, a screen resolution of 1920x1080 means that the screen has 1920 pixels in the X direction and 1080 pixels in the Y direction.

Here is an image of my laptop screen that I took from my phone camera at full zoom, and you can see the grid of pixels.

<p align="center">
  <img alt="pixels monitor photo" src="../imgs/pixels.png" width=400/>
</p>

## 1.2. Colour

A pixel consists of three sub pixels, A red, green and blue sub pixel. You can actually see this in the image above. It turns out, that most colours that the human eye can see can be made by just mixing red green and blue light together. For instance, on a digital screen, if you're looking at something white, it actually is red, green and blue light all mixed together. In the image above, you can see the white bracket has all of its sub pixels lit up.

Each sub pixel can have 255 different levels of brightness, ranging from 0 to 255 (both inclusive). These shades are shown below:

<p align="center">
  <img alt="red scale" src="../imgs/red.png" width=200/> <img alt="green scale" src="../imgs/green.png" width=200/> <img alt="blue scale" src="../imgs/blue.png" width=200/>
</p>

Thus, for every pixel, there are $256^3$ different possible combinations of colours that it can have.

This combination of red, green and blue values that make up the colour of the pixel is known as the RGB value of that pixel.

There is a special case for the RGB value of a pixel, where all three brightness levels are equal. When this happens, the pixel shows a shade of grey. This value is simply referred to as the greyscale value of the pixel

<p align="center">
  <img alt="grey scale" src="../imgs/greyscale.png" width=200/>
</p>

There is one more component of colour that can modify what a pixel looks like - transparancy. The transparancy value also ranges from 0-255, where 0 is fully transparant and 255 is fully opaque. The red square in both images has an alpha value of 255 (fully opaque) but the blue square in the left image has an alpha value of 150 (more opaque) and the blue square in the right image has an alpha value of 50 (more transparent)

<p align="center">
  <img alt="alpha = 150" src="../imgs/alpha150.png" width=200 height=200/> <img alt="alpha = 50" src="../imgs/alpha50.png" width=200 height=200/>
</p>

All of these four numbers, red, green, blue and alpha are collectively referred to as the RGBA value

## 1.3. Coordinates

To be able to draw anything on the screen, we want to be able to specify a position for it. For this reason, each pixel on the screen has some coordinates associated with it. These coordinates are represented in the Cartesian coordinate system. Conventionally, the coordinate system has its origin in the "centre" of the plane, but with computers, its slightly different. The origin, (0, 0), is at the top left of the screen and the positive X direction is towards the right and the positive Y direction is towards the bottom.

<p align="center">
  <img alt="computer screen coordinate system" src="http://www.jennyreadresearch.com/wp-content/uploads/2012/02/screencoords.jpg" width=400/>
</p>

The reason for this confusing difference is because early monitors were all CRT monitors, that drew each frame pixel by pixel from left to right and top to bottom. This made it easier to just have (0, 0) at the top left. This is an intersting video to watch if you want to learn more about how CRT monitors work:

<p align="center">
<iframe width="450" height="253" src="https://www.youtube.com/embed/3BJU2drrtCM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</p>