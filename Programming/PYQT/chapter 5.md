# Menus, Toolbars, and More

## NotePad GUI
```python 
import sys

from PyQt5.QtWidgets import (QApplication, QMainWindow,
                             QAction, QTextEdit, QFileDialog, QInputDialog,
                             QFontDialog, QColorDialog, QMessageBox)

from PyQt5.QtGui import QIcon, QTextCursor, QColor
from PyQt5.QtCore import Qt


class Notepad(QMainWindow):
    def __init__(self):
        super().__init__()
        self.initUI()

    def initUI(self):
        self.setGeometry(100, 100, 400, 500)
        self.setWindowTitle("Rich Notepad GUI")
        self.makeWidgets()
        self.show()

    def makeWidgets(self):
        self.text_field = QTextEdit()
        self.setCentralWidget(self.text_field)

        #### Making the Actions ####
        ## Actions for File Menu ##
        new_action = QAction(" New", self)
        new_action.setShortcut("Ctrl+N")
        new_action.triggered.connect(self.clearText)

        open_action = QAction(" Open", self)
        open_action.setShortcut("Ctrl+O")
        open_action.triggered.connect(self.openFile)

        save_action = QAction(" Save", self)
        save_action.setShortcut("Ctrl + S")
        save_action.triggered.connect(self.saveToFile)

        exit_action = QAction(" Exit", self)
        exit_action.setShortcut('Ctrl+Q')
        exit_action.triggered.connect(self.close)

        ## Actions for Edit Menu ##
        undo_action = QAction(' Undo', self)
        undo_action.setShortcut('Ctrl+Z')
        undo_action.triggered.connect(self.text_field.undo)

        redo_action = QAction(' Redo', self)
        redo_action.setShortcut('Ctrl+Shift+Z')
        redo_action.triggered.connect(self.text_field.redo)

        copy_action = QAction(' Copy', self)
        copy_action.setShortcut('Ctrl+C')
        copy_action.triggered.connect(self.text_field.copy)

        paste_action = QAction(' Paste', self)
        paste_action.setShortcut('Ctrl+V')
        paste_action.triggered.connect(self.text_field.paste)

        find_action = QAction(' Find', self)
        find_action.setShortcut('Ctrl+F')
        find_action.triggered.connect(self.findTextDialog)

        ## Actions for Tools Menu ##
        font_action = QAction(' Set Font', self)
        font_action.setShortcut('Ctrl+T')
        font_action.triggered.connect(self.chooseFont)

        color_action = QAction(" Set Color", self)
        color_action.setShortcut('Ctrl+Shift+C')
        color_action.triggered.connect(self.chooseFontColor)

        highlight_action = QAction('Highlight', self)
        highlight_action.setShortcut("Ctrl+Shift+H")
        highlight_action.triggered.connect(self.chooseFontBackgroundColor)

        about_action = QAction("About", self)
        about_action.triggered.connect(self.aboutDialog)

        ### Making The MENU BAR ###
        menu_bar = self.menuBar()

        ## Making File Menu and Adding the Actions ##
        file_menu = menu_bar.addMenu('File')
        file_menu.addAction(new_action)
        file_menu.addSeparator()
        file_menu.addAction(save_action)
        file_menu.addAction(open_action)
        file_menu.addSeparator()
        file_menu.addAction(exit_action)

        ## Making Edit Menu and Adding the Actions ##
        edit_menu = menu_bar.addMenu('Edit')
        edit_menu.addAction(undo_action)
        edit_menu.addAction(redo_action)
        edit_menu.addSeparator()
        edit_menu.addAction(copy_action)
        edit_menu.addAction(paste_action)
        edit_menu.addSeparator()
        edit_menu.addAction(find_action)

        ## Making Tools Menu and Adding the Actions ##
        tools_menu = menu_bar.addMenu('Menu')
        tools_menu.addAction(font_action)
        tools_menu.addAction(color_action)
        tools_menu.addAction(highlight_action)

    def openFile(self):
        file_name, _ = QFileDialog.getOpenFileName(
            self, 'Open File', "", "HTML Files (*html);; Text Files (*.txt)")

        if file_name:
            with open(file_name) as file:
                self.text_field.setText(file.read())
        else:
            QMessageBox.information(
                self, "Error", 'Unable to Open File', QMessageBox.Ok)

    def saveToFile(self):
        file_name, _ = QFileDialog.getSaveFileName(
            self, "Save File", "", "HTML Files (*.html) , Text Files (*.txt)")

        if file_name.endswith('.txt'):
            notepad_text = self.text_field.toPlainText()
            with open(file_name, "w") as file:
                file.write(notepad_text)

        else:
            QMessageBox.information(
                self, "Error", "Unable to save file", QMessageBox.Ok)

    def clearText(self):
        answer = QMessageBox.question(
            self, "Clear Text", "Do you want to clear this text", QMessageBox.No | QMessageBox.Yes, QMessageBox.Yes)
        if answer == QMessageBox.Yes:
            self.text_field.clear()

    def findTextDialog(self):
        find_text, ok = QInputDialog.getText(self, "Search Text", "Find:")
        extra_selections = []

        if ok and not self.text_field.isReadOnly():
            self.text_field.moveCursor(QTextCursor.Start)
            color = QColor(Qt.yellow)

            while self.text_field.find(find_text):
                selection = QTextEdit.ExtraSelection()
                selection.format.setBackground(color)

                selection.cursor = self.text_field.textCursor()

                extra_selections.append(selection)

            for i in extra_selections:
                self.text_field.setExtraSelections(extra_selections)

    def chooseFont(self):
        current = self.text_field.currentFont()
        font , ok = QFontDialog.getFont(current , self )
        if ok:
            self.text_field.setCurrentFont(font)

    def chooseFontColor(self):
        color = QColorDialog.getColor()
        if color.isValid():
            self.text_field.setTextColor(color)

    def chooseFontBackgroundColor(self):
        color = QColorDialog.getColor()
        if color.isValid():
            self.text_field.setTextBackgroundColor(color)

    def aboutDialog(self):
        QMessageBox.about(self, "About Notepad" , "Pyqt notepad project")


if __name__ == "__main__":
    app = QApplication(sys.argv)
    window = Notepad()
    sys.exit(app.exec_())
```

This notepad gui uses QMainWindow instead of QWidget class. QMainWindow is used to create more complex guis.

First we set the central widget.
Then we make actions for the all the menus.
Then we make all the menus and all the actions to them.

Actions can have a shortcut and trigger functions when user clicks on them.