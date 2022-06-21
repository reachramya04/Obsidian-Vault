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
