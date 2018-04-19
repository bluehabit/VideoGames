## Pixel Number Counter

In this first example we will demonstrate how to render part of an image to the canvas. 

Before we draw a bitmap of any sort to the canvas, we must first wait for the image to load. Otherwise, the `drawImage()` method will not work correctly. 

![f](https://imgur.com/a/B57tq.png)

Demo: https://codepen.io/bluehabit/pen/KRKjbB

### `ctx.drawImage()`

![f](https://imgur.com/xRL4cWR.png)

MDN page: https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/drawImage

Lets familiarize ourselves with `drawImage()` syntax. Note, this method has distinct coordinate groups. One group is `sx` and `sy`, this represents the `x,y` coordinate on the source image, in our case the sprite sheet bitmap.  The other group is `dx` and `dy`. This group represents the coordinates on the destination canvas. 

We are effectively cutting pieces from the source image like a cookie cutter. Where the source image can be thought of as our raw dough, and the coordinates represent a cookie cutter. The `sx` `sy` coordinates will determine the shape we cut out from our source dough.

Based on these coordinates that we pass through will determine the shape we cut out. The `dx` and `dy` coordinates will determine where our cut out shape will be placed on our final baking sheet.

### Sprite Cutter Constructor Function

In this example, even though we are using a constructor function to cut out our sprite sheet, we still put its custom `draw()` method within the `load` event of the sprite sheet. Just like before, the source bitmap must first load before we can do anything with it. As shown here `smallNum.draw(55, 105)` 

Notice how we modify the coordinates a bit, such that the `sx` and `sy` coordinates in the source image now represent the position of the number `2`. 

In addition notice we added the class `spriteCookieCutter`, which has a shared method on the prototype named `draw`. This is modular code we can use to input any image, and use a 'cookie cutter' in the form of coordinates to cut a piece out from the source image and paste it on our canvas where we please.

```
class spriteCookieCutter {
	constructor(img, x, y, width, height){
		this.img = img;
		this.x = x;
		this.y = y;
		this.width = width;
		this.height = height;
	}

	draw(x, y){
		ctx.drawImage(this.img, this.x, this.y, this.width, this.height, x, y, this.width, this.height);
	}
}
```

![f](https://imgur.com/yzfqtjE.png)

Demo: https://codepen.io/bluehabit/pen/WJNVoY
  
---

Putting up the finishing touches on our code, we have added a `for` loop to the `draw` function. This loop will accept a number from the user to draw to the canvas, for example a high score of `2205`. 

The function will then take the users input, and convert it to a string. The reason for this is it allows us to use the `.length` property of a string to easily manipulate the data.

Because each digit `0-9` corresponds to a very specific coordinate section on the sprite sheet we can use `step * n` to render a specific number to the screen. 

Lastly we have `x += step`. This is important, without it the program will keep overwriting the same space on the canvas until it reaches the last number in the string. Remember we can think of function arguments as locally created variables that exist only within the scope of that function. Using that logic, we can just reassign `x` each time through the loop and increment it for every step we take. This will render and 'push it over' allowing us to render new numbers.

![f](https://imgur.com/HseI0VP.png)

Demo: https://codepen.io/bluehabit/pen/ELaYYm


### Reasoning Behind Numbers

**Legend**

Below is a blown up version of our source sprite number sheet so we can more easily distinguish individual pixels from one another. Notice in the upper left hand corner we are starting at `x:0, y:0`. 

![f](https://imgur.com/ryrcdaO.png)

---

There are very specific reasons we chose these numbers when referencing coordinates from the source image. For instance, the gap between each block of numbers is `2 pixels` that is why `step = this.width + 2`. 

![f](https://imgur.com/9bCGjN9.png)

