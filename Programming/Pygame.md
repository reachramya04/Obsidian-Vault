# Introductory Loop
```python
import pygame as pg 
import sys 

pg.init()
screen = pg.display.set_mode((screen_width , screen_height))
clock = pg.time.Clock()


while True:
	for event in pg.event.get():
		if event.type == pg.QUIT:
			pg.quit()
			sys.exit()
			
	screen.fill('black')
	pg.display.update()
	clock.tick(fps)
```

`pg.init()` initializes  all the modules required for running the whole code.
`screen` var is the main var on which all the blitting of sprites/rectangles takes place.
	- It takes in a tuple of *screen_width* and *screen_height*.
	- *screen.fill()* colors the screen with black color. 
`clock` var is used to set the default value of fps for the pygame window , without this the fps will always be the maximum considering what the CPU allows. 
	 - *clock.tick(fps)* takes in the fps argument as integer , standard is 60.

The `for` loop inside the *while True* loop is used to close the pygame window when the close button is pressed.
Without this the pygame window wont close.



