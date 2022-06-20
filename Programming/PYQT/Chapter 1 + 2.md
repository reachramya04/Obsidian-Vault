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
- `self.initUI()` is a good practice to combine all the window calls in one place.

## QLabel and QPixmap
```python
import sys 
from PyQt5.QtWidgets import QApplication , QWidget , QLabel 
from PyQt5.QtGui import QPixmap

class HelloWorldWindow(QWidget):
	def __init__(self):
		super().__init__()
		self.initUI()
		
	def initUI(self):
		self.setGeometry(100,100,250,250)
		self.setWindowTitle("Windoe Titl")
		self.displayLabels()
		self.show()
		
	def displayLabels(self):
		text = QLabel(self)
		text.setText("Hello")
		text.move(105,15)
		image = "/hdd/Downloads/BS Stuff/earth.png"
		try:
			with open(image):
				image_widget = QLabel(self)
				pixmap = QPixmap(image)
				image_widget.setPixmap(pixmap)
				image_widget.move(25,40)
		except FileNotFoundError:
			print("Image aint there lol")	

if __name__=="__main__":
	app = QApplication(sys.argv)
	window = HelloWorldWindow()
	sys.exit(app.exec_())
```

- `self.displayLabels()` creates the *Hello* Label and creates another Label with Pixmap of the earth image.
- `image_widget` is set to a *QLabel* Instance and then a method `setPixmap()` is called to set it to an image.
- It is to be noted that a `Pixmap(file_path)` is passed in `setPixmap()` to load in the image. (file_path is path to the image) 
- `move` method is called to position the widgets onto the main widget , its a part of absolute positioning and may break somtimes.

## Simple User GUI
```python 
import sys 
from PyQt5.Widgets import QApplication , QLabel , QWidget
from PyQt5.QtGui import QFont , QPixmap 

class UserProfile(QWidget):
	def __init__(self):
		super().__init__()
		self.initUI()
		
	def initUI(self):
		self.setGeometry(50,50,250,400):
		self.setWindowTitle("USER PROFILE")
		self.displayImages()
		self.displayLabels()
		self.show()
		
	def displayImages(self):
		profile_image = '/hdd/Downloads/BS Stuff/profile.png'
		try:
			with open(profile_image):
				profile_image_widget = QLabel(self)
				pixmap = QPixmap(profile_image)
				profile_image_widget.setPixmap(pixmap)
				profile_image_widget.move(80,20)
		except FileNotFoundError:
			print("File aint there lol")
			
	def displayLabels(self):
		user_name = QLabel(self)
		user_name.setText("John Doe")
		user_name.move(85, 140)
		user_name.setFont(QFont('SpaceMono Nerd Font', 20))
		bio_title = QLabel(self)
		bio_title.setText("Biography")
		bio_title.move(15, 170)
		bio_title.setFont(QFont('SpaceMono Nerd Font', 17))
		about = QLabel(self)
		about.setText("I'm a Software Engineer with 8 years\
		experience creating awesome code.")
		about.setWordWrap(True)
		about.move(15, 190)
		skills_title = QLabel(self)
		skills_title.setText("Skills")
		skills_title.move(15, 240)
		skills_title.setFont(QFont('SpaceMono Nerd Font', 17))
		skills = QLabel(self)
		skills.setText("Python | PHP | SQL | JavaScript")
		skills.move(15, 260)
		experience_title = QLabel(self)
		experience_title.setText("Experience")
		experience_title.move(15, 290)
		experience_title.setFont(QFont('SpaceMono Nerd Font', 17))
		experience = QLabel(self)
		experience.setText("Python Developer")
		experience.move(15, 310)
		dates = QLabel(self)
		dates.setText("Mar 2011 - Present")
		dates.move(15, 330)
		dates.setFont(QFont('SpaceMono Nerd Font', 10))
		experience = QLabel(self)
		experience.setText("Pizza Delivery Driver")
		experience.move(15, 350)
		dates = QLabel(self)
		dates.setText("Aug 2015 - Dec 2017")
		dates.move(15, 370)
		dates.setFont(QFont('SpaceMono Nerd Font', 10))

if __name__ == "__main__":
	app = QApplication(sys.argv)
	window = UserProfile()
	sys.exit(app.exec_())
```
- `setFont()` method is called to change the font of the given label to another font.
- An instance of `QFont(Font_name , )`



