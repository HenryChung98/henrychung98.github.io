---
layout: single
title: "GPA Calculator Project Process_1"
categories: project
tags: [python, tkinter, gpa_calculator]
author_profile: false
search: true
use_math: true
---

### introduction

GPA stands for 'Grade Point Average', a number that indicates how high you scored in your courses on average.
For example, assume the highest grade is A+(4.33), and if you have taken 3 courses with A(4.0), B(3.0), A+(4.33), then your current GPA is
$\(\(4.0 + 3.0 + 4.33\) / 3 = 3.76\)$

Python has a library called tkinter to construct basic graphical user interface (GUI) applications.
I will use this library and make GPA calculator.

### Code

#### import

```python
from tkinter import * # GUI
from tkinter import ttk # for combo box
from tkinter.messagebox import * # for message box
```

#### initialization

```python
class MyGUI:
    def __init__(self):
        self.mainWindow = Tk()
        self.windowWidth = 700
        self.windowHeight = 220 # variable to resize window height
        self.mainWindow.geometry(f"700x{self.windowHeight}+720+50")
        self.mainWindow.title("GPA Calculator")

        # initialize grade values
        self.gradeValue = ["A+", "A", "A-", "B+", "B", "B-", "C+", "C", "C-", "D", "F"]

        # frame for header
        self.frame1 = Frame(self.mainWindow, width=520, height=30, bg="#d2302c")
        self.frame1.place(x=20, y=30)

        # frame for input course name, grade
        self.frame2Height = 100 # variable to resize frame2 height
        self.frame2 = Frame(self.mainWindow, width=520, height=self.frame2Height, bg="#f4a896")
        self.frame2.place(x=20, y=60)

        # frame for buttons
        self.frame3 = Frame(self.mainWindow, width=100, height=180)
        self.frame3.place(x=560, y=30)
```

#### place header

```python
self.courseLabel = Label(self.frame1, text="Course", font=14, fg="white", bg="#d2302c")
self.courseLabel.place(x=10, y=5)
self.gradeLabel = Label(self.frame1, text="Grade", font=14, fg="white", bg="#d2302c")
self.gradeLabel.place(x=113, y=5)
self.includeLabel = Label(self.frame1, text="Included", font=14, fg="white", bg="#d2302c")
self.includeLabel.place(x=180, y=5)
self.courseLabel2 = Label(self.frame1, text="Course", font=14, fg="white", bg="#d2302c")
self.courseLabel2.place(x=280, y=5)
self.gradeLabel2 = Label(self.frame1, text="Grade", font=14, fg="white", bg="#d2302c")
self.gradeLabel2.place(x=383, y=5)
self.includeLabel2 = Label(self.frame1, text="Included", font=14, fg="white", bg="#d2302c")
self.includeLabel2.place(x=450, y=5)
```

#### place buttons

```python

# for radio button
self.choice=StringVar()
self.choice.set("RED") # set initial color red

# radio buttons to change background color
self.rb1=Radiobutton(self.frame3, text="Red", font=14, variable=self.choice, value="RED", command=self.changeBgr)
self.rb1.place(x=10, y=70)
self.rb2=Radiobutton(self.frame3, text="Green", font=14, variable=self.choice, value="GREEN", command=self.changeBgg)
self.rb2.place(x=10, y=100)
self.rb3=Radiobutton(self.frame3, text="Blue", font=14, variable=self.choice, value="BLUE", command=self.changeBgb)
self.rb3.place(x=10, y=130)

# add course button(input structures for course name, grade will be added)
self.addCourseButton = Button(self.frame3, text="Add Course", font=("Arial", 14), width=7, command=self.addCourse)
self.addCourseButton.place(x=10, y=10)

# calculate your current GPA button
self.calculateButton = Button(self.frame3, text="Calculate", font=("Arial", 14), width=7, command=self.calculateGPA)
self.calculateButton.place(x=10, y=40)
```

#### input structures

```python

# course name
self.course = Entry(self.frame2, width=10, bg="#f4a896", fg="black")
self.course.place(x=10, y=5)

# your grade of the course
self.grade = ttk.Combobox(self.frame2, values=self.gradeValue, width=3)
self.grade.place(x=113, y=5)
self.grade.set(self.gradeValue[0]) # initial value A+

# check button to include or not when calculating
self.include=IntVar()
self.include.set(1) # prechecked
self.cb = Checkbutton(self.frame2, width=3, variable=self.include, font=14, bg="#f4a896")
self.cb.place(x=195, y=5)

```
