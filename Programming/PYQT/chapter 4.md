# Layout Management
## Types of layouts
- Absolute positioning with *move()*.
- *QBoxLayout* which is useful for creating simple GUIs with horizontal or vertical layouts.
- *QFormLayout* is a convenience layout useful for making application forms.
- *QGridLayout* allows for more control over arranging widgets by specifying x and y coordinate values.

### QHBoxLayout and QVBoxLayout
```python
import sys
from PyQt5.QtWidgets import (
    QApplication, QWidget, QLabel,
    QMessageBox, QPushButton, QHBoxLayout,
    QCheckBox, QVBoxLayout, QButtonGroup)
from PyQt5.QtGui import QFont


class surveyGUI(QWidget):
    def __init__(self):
        super().__init__()
        self.initUI()

    def initUI(self):
        self.setGeometry(100, 100, 400, 250)
        self.setWindowTitle("Survey GUI")
        self.displayWidgets()
        self.show()

    def displayWidgets(self):
        title = QLabel("Resturant Name", self)
        title.setFont(QFont("space mono nerd font", 16))

        question = QLabel("How would you rate our service today?", self)
        title_hbox = QHBoxLayout() 
        title_hbox.addStretch()
        title_hbox.addWidget(title)
        title_hbox.addStretch()

        ratings = ["good" , "bad" , "worst"]
        ratings_hbox = QHBoxLayout()
        ratings_hbox.setSpacing(60)
        ratings_hbox.addStretch()

        for rating in ratings:
            rate_label = QLabel(rating ,self)
            ratings_hbox.addWidget(rate_label)
        ratings_hbox.addStretch()

        cb_hbox = QHBoxLayout()
        cb_hbox.setSpacing(100)
        scale_bg = QButtonGroup(self)

        cb_hbox.addStretch()
        for cb in range(len(ratings)):
            scale_cb = QCheckBox(str(cb) , self)
            cb_hbox.addWidget(scale_cb)
            scale_bg.addButton(scale_cb)
        cb_hbox.addStretch()
    
        vbox = QVBoxLayout()
        vbox.addLayout(title_hbox)
        vbox.addWidget(question)
        vbox.addStretch(1)
        vbox.addLayout(ratings_hbox)
        vbox.addLayout(cb_hbox)
        vbox.addStretch(2)

        self.setLayout(vbox)

if __name__ == "__main__":
    app = QApplication(sys.argv)
    window = surveyGUI()
    sys.exit(app.exec_())
```

This example uses *QHBoxLayout* and *QVBoxLayout*
The basically first makes widgets and then adds them to *QHBoxLayout* then we create a vertical layout and add all the widgets and layouts to the vertical layout.
At the end the main layout of the widget app is set to the vertical layout.

`addStretch()` method adds a resizable blank space.
`setSpacing()` sets a permanent distance between the widgets of the layout.

`QButtonGroup` is used to makes the checkboxes mutually exclusive. It means that only one of them can be checked at a time.

## QComboBox and QSpinBox
*QComboBox* is like a dropdown menu to select items.
*QSpinBox* is used to select a range of integer values.

```python
import sys
from PyQt5.QtWidgets import (
    QApplication, QMainWindow, QWidget, QLabel,
    QPushButton, QHBoxLayout,
    QCheckBox, QVBoxLayout, QComboBox, QSpinBox)
from PyQt5.QtGui import QFont
from PyQt5.QtCore import Qt


class foodGUI(QWidget):
    def __init__(self):
        super().__init__()
        self.initUI()

    def initUI(self):
        self.setGeometry(100, 100, 300, 200)
        self.setWindowTitle("FOOD ITEM GUI")
        self.displayWidgets()
        self.show()

    def displayWidgets(self):
        ### DEFINING WIDGETS ###
        title = QLabel("Select the food items", self)
        title.setFont(QFont("space mono nerdfont", 15))

        food_items = ["egg", "turkey sandwich", "ham sandwich",
                      "cheese", "hummus", "yogurt", "apple", "banana", "orange",
                      "waffle", "baby carrots", "bread", "pasta", "crackers",
                      "pretzels", "pita chips", "coffee", "soda", "water"]

        food_selector1 = QComboBox()
        food_selector1.addItems(food_items)
        self.food_price1 = QSpinBox()
        self.food_price1.setRange(0, 100)
        self.food_price1.setPrefix("$")
        self.food_price1.valueChanged.connect(self.displayTotal)

        food_selector2 = QComboBox()
        food_selector2.addItems(food_items)
        self.food_price2 = QSpinBox()
        self.food_price2.setRange(0, 100)
        self.food_price2.setPrefix("$")
        self.food_price2.valueChanged.connect(self.displayTotal)

        self.total_cost = QLabel("Total Spent : $0", self)

        ### DEFINING LAYOUTS AND ADDING WIDGETS ###
        title_hbox = QHBoxLayout()
        title_hbox.addStretch()
        title_hbox.addWidget(title)
        title_hbox.addStretch()

        food_hbox1 = QHBoxLayout()
        food_hbox1.addStretch()
        food_hbox1.addWidget(food_selector1)
        food_hbox1.addStretch(20)
        food_hbox1.addWidget(self.food_price1)
        food_hbox1.addStretch()

        food_hbox2 = QHBoxLayout()
        food_hbox2.addStretch()
        food_hbox2.addWidget(food_selector2)
        food_hbox2.addStretch(20)
        food_hbox2.addWidget(self.food_price2)
        food_hbox2.addStretch()

        main_vbox = QVBoxLayout()
        main_vbox.addStretch()
        main_vbox.addLayout(title_hbox)
        main_vbox.addStretch()
        main_vbox.addLayout(food_hbox1)
        main_vbox.addStretch()
        main_vbox.addLayout(food_hbox2)
        main_vbox.addStretch()
        main_vbox.addWidget(self.total_cost)

        self.setLayout(main_vbox)

    def displayTotal(self):
        total_amount = self.food_price1.value() + self.food_price2.value()
        self.total_cost.setText(f"Total Spent : {total_amount}")


if __name__ == "__main__":
    app = QApplication(sys.argv)
    window = foodGUI()
    sys.exit(app.exec_())
```

The methods in this example are self explanatory.

## Appointment GUI 
```python 
import sys
from PyQt5.QtWidgets import (QApplication, QFormLayout, QHBoxLayout, QPushButton, QLineEdit,
                             QLabel, QComboBox, QSpinBox, QTextEdit, QWidget
                             )
from PyQt5.QtGui import QFont, QIntValidator


class appointmentGUI(QWidget):
    def __init__(self):
        super().__init__()
        self.initUI()

    def initUI(self):
        self.setGeometry(100,100,300,400)
        self.setWindowTitle("Appointment Booking GUI")
        self.displayWidgets()
        self.show()

    def displayWidgets(self):
        ### DEFINING WIDGETS ###
        title_label = QLabel("Appointment Submission Form", self)
        self.name_entry = QLineEdit()
        self.address_entry = QLineEdit()
        self.phoneno_entry = QLineEdit()
        self.phoneno_entry.setInputMask("0000-000-000;")

        age_label = QLabel("Age", self)
        self.age_entry = QSpinBox()
        self.age_entry.setRange(0, 100)

        height_label = QLabel("Height", self)
        self.height_entry = QLineEdit()
        self.height_entry.setPlaceholderText("cm")

        weight_label = QLabel("Weight", self)
        self.weight_entry = QLineEdit()
        self.weight_entry.setPlaceholderText("kg")

        self.gender_entry = QComboBox()
        self.gender_entry.addItems(["Male", "Female", "Mentall Ill Genders"])

        self.past_surgery_entry = QTextEdit()

        self.blood_type_entry = QComboBox()
        self.blood_type_entry.addItems(["A", "B", "C", "D"])

        self.desired_time_entry = QLineEdit()
        self.desired_time_entry.setInputMask("00:00")
        self.desired_time_entry_ampm = QComboBox()
        self.desired_time_entry_ampm.addItems(["AM", "PM"])

        self.submit_button = QPushButton()
        self.submit_button.setText("Submit Appointment")

        ### DEFINING LAYOUTS AND ADDING WIDGETS ###
        hbox1 = QHBoxLayout()
        hbox1.addStretch()
        hbox1.addWidget(age_label)
        hbox1.addWidget(self.age_entry)
        hbox1.addStretch()
        hbox1.addWidget(height_label)
        hbox1.addWidget(self.height_entry)
        hbox1.addStretch()
        hbox1.addWidget(weight_label)
        hbox1.addWidget(self.weight_entry)
        hbox1.addStretch()

        hbox2 = QHBoxLayout()
        hbox2.addStretch()
        hbox2.addWidget(self.desired_time_entry)
        hbox2.addWidget(self.desired_time_entry_ampm)
        hbox2.addStretch()

        main_form_layout = QFormLayout()
        main_form_layout.addRow(title_label)
        main_form_layout.addRow("Full Name", self.name_entry)
        main_form_layout.addRow("Address", self.address_entry)
        main_form_layout.addRow("Mobile Number", self.phoneno_entry)
        main_form_layout.addRow(hbox1)
        main_form_layout.addRow("Gender", self.gender_entry)
        main_form_layout.addRow("Past Surgeries", self.past_surgery_entry)
        main_form_layout.addRow("Blood Type", self.blood_type_entry)
        main_form_layout.addRow("Desired Time", hbox2)
        main_form_layout.addRow(self.submit_button)

        self.setLayout(main_form_layout)


if __name__ == "__main__":
    app = QApplication(sys.argv)
    window = appointmentGUI()
    sys.exit(app.exec_())
```

This exercise was to test how much I had learnt.
The only new thing here is the `QFormLayout`

```
QFormLayout.addRow("Text" , widget/layout)
```

This is used to add a row in the formlayout.
The text is shown on the left side of widget/layout.

Also `setInputMask` method is used to limit the number of characters in a *QLineEdit Widget*.


### QGridLayout
The QGridLayout layout manager is used to arrange widgets in rows and columns similar to a spreadsheet or matrix. The layout manager takes the space within its parent
window or widget and divides it up according to the sizes of the widgets within that row (or column). Adding space between widgets, creating a border, or stretching widgets
across multiple rows or columns is also possible.

### Todo List GUI 
```python 
# todolist.py
# Import necessary modules
import sys
from PyQt5.QtWidgets import (QApplication, QWidget, QLabel,
QTextEdit, QLineEdit, QPushButton, QCheckBox, QGridLayout,
QVBoxLayout)
from PyQt5.QtGui import QFont
from PyQt5.QtCore import Qt

class ToDoList(QWidget):
	def __init__(self): # Constructor
		super().__init__()
		self.initializeUI()
		
	def initializeUI(self):
		"""
		Initialize the window and display its contents to the
		screen
		"""
		self.setGeometry(100, 100, 500, 350)
		self.setWindowTitle('4.4 – ToDo List GUI')
		self.setupWidgets()
		self.show()
		
	def setupWidgets(self):
		"""
		Create widgets for to-do list GUI and arrange them in
		the window
		"""
		# Create grid layout
		main_grid = QGridLayout()
		todo_title = QLabel("To Do List")
		todo_title.setFont(QFont('Arial', 24))
		todo_title.setAlignment(Qt.AlignCenter)
		close_button = QPushButton("Close")
		close_button.clicked.connect(self.close)
		
		# Create section labels for to-do list
		mustdo_label = QLabel("Must Dos")
		mustdo_label.setFont(QFont('Arial', 20))
		mustdo_label.setAlignment(Qt.AlignCenter)
		appts_label = QLabel("Appointments")
		appts_label.setFont(QFont('Arial', 20))
		appts_label.setAlignment(Qt.AlignCenter)
		
		# Create must-do section
		mustdo_grid = QGridLayout()
		mustdo_grid.setContentsMargins(5, 5, 5, 5)
		mustdo_grid.addWidget(mustdo_label, 0, 0, 1, 2)
		
		# Create checkboxes and line edit widgets
		for position in range(1, 15):
			checkbox = QCheckBox()
			checkbox.setChecked(False)
			linedit = QLineEdit()
			linedit.setMinimumWidth(200)
			mustdo_grid.addWidget(checkbox, position, 0)
			mustdo_grid.addWidget(linedit, position, 1)
			
		# Create labels for appointments section
		morning_label = QLabel("Morning")
		morning_label.setFont(QFont('Arial', 16))
		morning_entry = QTextEdit()
		noon_label = QLabel("Noon")
		noon_label.setFont(QFont('Arial', 16))
		noon_entry = QTextEdit()
		evening_label = QLabel("Evening")
		evening_label.setFont(QFont('Arial', 16))
		evening_entry = QTextEdit()
		
		# Create vertical layout and add widgets
		appt_v_box = QVBoxLayout()
		appt_v_box.setContentsMargins(5, 5, 5, 5)
		appt_v_box.addWidget(appts_label)
		appt_v_box.addWidget(morning_label)
		appt_v_box.addWidget(morning_entry)
		appt_v_box.addWidget(noon_label)
		appt_v_box.addWidget(noon_entry)
		appt_v_box.addWidget(evening_label)
		appt_v_box.addWidget(evening_entry)
		
		# Add other layouts to main grid layout
		main_grid.addWidget(todo_title, 0, 0, 1, 2)
		main_grid.addLayout(mustdo_grid, 1, 0)
		main_grid.addLayout(appt_v_box, 1, 1)
		main_grid.addWidget(close_button, 2, 0, 1, 2)
		self.setLayout(main_grid)


if __name__ == "__main__":
app = QApplication(sys.argv)
window = ToDoList()
sys.exit(app.exec_())
```

First the QLineEdit and QCheckBox widgets are added using the for loop into the sub-gird layout `mustdo_grid`
Then the appointments widgets are added into a QVBoxLayout called `appt_v_box`.
Then all of this is added to the main grid layout.

The `addWidget()` Method for QGridLayout takes following arguments.
`QGridLayout.addWidget(widget , Row , Column , Span_row , Span_column)`
`Span_row` and `Span_column` are optional.
They stretch the widget to occupy that many rows and columns.

Similarly `addLayout()` method can be used to add layouts to the main grid layout.
