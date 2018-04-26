## Repainting 

When we animate video games using canvas, we are often using a built in method `window.requestAnimationFrame(run)`. According to the MDN article the number of callbacks is usually `60 times per second`, or `60 fps` in videogame lingo. Everytime we update a frame, we must repaint its new position to give the illusion of animation.

## Why Repainting is Important

If we do not repaint the canvas every frame, then the canvas will never refresh. As a result it will create this ghosting like effect where the image itself will trail many times across the canvas. 

Repainting, is like updating the canvas every single frame. In this way, the canvas will only display the newest most relevant information and will not contain old information like the previous position of the sprite (ghosting) that occurs when no repaint is set. 

![f](https://imgur.com/EJ92S0q.gif)

### Repainting Methods

### `fillRect`

If you are filling the background with a specific color, this is the recommended method to repaint the screen. For example if we have this example using flappy bird where we are using a blue background, if we attempt to use `clearRect` it will clear the blue background (`#70c5cf`) we set with `fillRect`. As shown below.




### `clearRect`

If you are not filling the background of the canvas with a particular color then this option is fine to use. 
