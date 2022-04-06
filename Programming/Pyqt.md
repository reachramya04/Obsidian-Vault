# Starting with PyQT 😄

## Creating an empty window for christs sake
```python
import sys
from PyQt5.QtWidgets import QApplication , QWidget

class EmptyWindow(QWidget):
	def __init__(self):
		super().__init__()
		
		self.initUI()
		
	def initUI(self):
		self.setGeometry(100 , 100 , 400 , 200)
		self.setWindowTitle("EMPTEE BINBOW")
		self.show()
		
if __name__ == "__main__":
	app = QApplication(sys.argv)
	window = EmptyWindow()
	sys.exit(app.exec_())
```

- `self.setGeometry(100 , 100 , 400 , 200)` the first 2 arguments in this line are the position of the window on the screen and `400` is the width of the window and `200` is the height of the window.
- also the top left of both the screen and the window is considered `0,0` according to the coordinate system.
- `self.show()` shows all the windows on the screen , anything after that doesnt show up on the main screen.
- `self.initUI()` is a good practice to combine all the window calls in one place 