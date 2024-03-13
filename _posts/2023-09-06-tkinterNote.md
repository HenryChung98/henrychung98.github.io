---
layout: single
title: "Python Tkinter"
categories: note
tags: [python, tkinter]
author_profile: false
search: true
---

### Introduction

tkinter is a Python library that can be used to construct basic graphical user interface (GUI) applications.

### Import

```python
from tkinter import *
```

### Initialization

e.g.

```python
class MyGUI:
def __init__(self): # constructor(self = this)
self.myWindow = Tk()
self.myWindow.geometry("300x300+100+100") # width x height + left + top

        self.myWindow.title("title") # title

        self.frame1 = Frame(self.myWindow, width = 280, height = 140, bg="yellow")
        self.frame1.place(x=10, y=10)

        self.frame2 = Frame(self.myWindow, width = 280, height = 140, bg="green")
        self.frame2.place(x=10, y=150)

        # positioned based on frame2 / fg = fontColor / bg = backgroundColor
        self.label = Label(self.frame2, text="Hello World", fg="yellow", bg="green")
        self.label.place(x=10, y=10)

        mainloop() # keeps the program running

myGui = MyGUI() # calling constructor(default)
```

[more info](https://docs.python.org/3/library/tkinter.html)

### Inputs

There are several input methods
But before we go, you may want to import messagebox library to check input is successfully entered.

```python
from tkinter.messagebox import * # for message box
```

#### Button

```python

# button to call the function
self.button1 = Button(self.frame1, text="Click Me!", command=self.doThis)
self.button1.place(x=20, y=50) # need to place the button

# button to quit the program
self.button2 = Button(self.frame1, text="Quit", command=self.myWindow.destroy)
self.button2.place(x=20, y=120) # need to place the button

def doThis(self):
    showinfo("Response", "Thanks for clicking") # show information box
    showerror("Response", "Thanks for clicking") # show error box(warning)
```

#### Entry

```python

# will display entry box
self.entry = Entry(self.frame1, width=10, font=14)
self.entry.place(x=60, y=90)

self.button1 = Button(self.frame1, text="Click me", font=14, command=self.doThis)
self.button1.place(x=60, y=140)


def doThis(self):
    theText=self.entry.get() # getting value from the entry box
    showinfo("Response", "You have entered " + theText)

```

#### Radio Button

```python
self.choice=StringVar() # getting value from the radio button
self.choice.set("TEA") # setting the initial value

self.rb1=Radiobutton(self.frame1, text="Tea", font=14, variable=self.choice, value="TEA", command=self.doThis)
self.rb1.place(x=40, y=40)

self.rb2=Radiobutton(self.frame1, text="Coffee", font=14, variable=self.choice, value="COFFEE", command=self.doThis)
self.rb2.place(x=40, y=75)

self.rb3=Radiobutton(self.frame1, text="Mocha", font=14, variable=self.choice, value="MOCHA", command=self.doThis)
self.rb3.place(x=40, y=110)


# each radio button has command=self.doThis, so when the radio button is clicked, this function is called
def doThis(self):
    showinfo("Response", str(self.choice.get()))
```

#### Check Button

```python
self.choice1=IntVar()
self.choice1.set(1)  # prechecked
self.choice2=IntVar()
self.choice2.set(0) # prechecked(unchecked)


self.cb1=Checkbutton(self.frame1, text="Tea", font=14, variable=self.choice1, command=self.do_this1)
self.cb1.place(x=40, y=40)

self.cb2=Checkbutton(self.frame1, text="Coffee", font=14, variable=self.choice2, command=self.do_this2)
self.cb2.place(x=40, y=75)

# when cb1 is clicked, this function is called
def do_this1(self):
    if self.choice1.get():
        showinfo("Response", "You like tea") # if selected, activated
    else:
        showinfo("Response", "You don't like tea") # if unselected, activated

# when cb2 is clicked, this function is called
def do_this2(self):
    if self.choice2.get():
        showinfo("Response", "You like coffee") # if selected, activated
    else:
        showinfo("Response", "You don't like coffee") # if unselected, activated

```

[More info](https://python-course.eu/tkinter/)
