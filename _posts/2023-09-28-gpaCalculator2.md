---
layout: single
title: "GPA Calculator Project Process_2"
categories: project
tags: [python, tkinter, gpa_calculator]
author_profile: false
search: true
---

We have set everything we need before we work for functions.
Now we need to create functions for

<div class="notice--info">
    <ul>
        <li>change background color</li>
        <li>add input structures</li>
        <li>calculate GPA</li>
     </ul>
</div>

### functions

#### variables

variables for functions

```python
# to give different value to each new inputs
self.gradeList = [self.grade]
self.includeList = [self.include]
self.courseList = [self.course]
self.cbList = [self.cb]

self.newPos = 5 # variable to display new inputs
self.checkBg = 0 # check background color
self.courseNum = 1
```

#### change background color

```python
def changeBgr(self): # change background red
    self.frame1.config(bg="#d2302c")
    self.frame2.config(bg="#f4a896")
    self.course.config(bg="#f4a896")
    self.cb.config(bg="#f4a896")
    self.courseLabel.config(bg="#d2302c")
    self.gradeLabel.config(bg="#d2302c")
    self.includeLabel.config(bg="#d2302c")
    self.courseLabel2.config(bg="#d2302c")
    self.gradeLabel2.config(bg="#d2302c")
    self.includeLabel2.config(bg="#d2302c")


    for i in self.courseList:
        i.config(bg="#f4a896")
    for i in self.cbList:
        i.config(bg="#f4a896")
    self.checkBg = 0


def changeBgg(self): # change background green
    self.frame1.config(bg="#17553b")
    self.frame2.config(bg="#ced46a")
    self.course.config(bg="#ced46a")
    self.cb.config(bg="#ced46a")
    self.courseLabel.config(bg="#17553b")
    self.gradeLabel.config(bg="#17553b")
    self.includeLabel.config(bg="#17553b")
    self.courseLabel2.config(bg="#17553b")
    self.gradeLabel2.config(bg="#17553b")
    self.includeLabel2.config(bg="#17553b")

    for i in self.courseList:
        i.config(bg="#ced46a")
    for i in self.cbList:
        i.config(bg="#ced46a")
    self.checkBg = 1

def changeBgb(self): # change background blue
    self.frame1.config(bg="#1663b2")
    self.frame2.config(bg="#9cc3d5")
    self.course.config(bg="#9cc3d5")
    self.cb.config(bg="#9cc3d5")
    self.courseLabel.config(bg="#1663b2")
    self.gradeLabel.config(bg="#1663b2")
    self.includeLabel.config(bg="#1663b2")
    self.courseLabel2.config(bg="#1663b2")
    self.gradeLabel2.config(bg="#1663b2")
    self.includeLabel2.config(bg="#1663b2")

    for i in self.courseList:
        i.config(bg="#9cc3d5")
    for i in self.cbList:
        i.config(bg="#9cc3d5")
    self.checkBg = 2
```

#### add input structures

```python
# to resize frames
if self.courseNum % 2 == 1:
    self.frame2Height += 25
    self.courseNum += 1
if self.frame2Height >= self.windowHeight - 50:
    self.windowHeight += 25
    self.frame2.config(height=self.frame2Height - 50)
    self.mainWindow.geometry(f"700x{self.windowHeight + 25}+720+50")


if self.courseNum == 61: # to limit the number of input structures
    showerror("ERROR", "TOO MANY COURSES")
else:
    self.newCourse = Entry(self.frame2, width=10, fg="black")
    self.courseList.append(self.newCourse)
    self.newGrade = ttk.Combobox(self.frame2, values=self.gradeValue, width=3)
    self.newGrade.set(self.gradeValue[0])
    self.gradeList.append(self.newGrade)
    self.newInclude=IntVar()
    self.newInclude.set(1)
    self.includeList.append(self.newInclude) # make sure included
    self.newCb = Checkbutton(self.frame2, width=3, variable=self.newInclude, font=14)
    self.cbList.append(self.newCb)

# to place the structures left, right, left, right ...
if self.courseNum % 2 == 1:
    self.newCourse.place(x=10, y=self.newPos)
    self.newGrade.place(x=113, y=self.newPos)
    self.newCb.place(x=195, y=self.newPos)
else:
    self.newCourse.place(x=280, y=self.newPos)
    self.newGrade.place(x=383, y=self.newPos)
    self.newCb.place(x=470, y=self.newPos)

# to match the background color
if self.checkBg == 0:
    for i in self.courseList:
        i.config(bg="#f4a896")
    for i in self.cbList:
        i.config(bg="#f4a896")

elif self.checkBg == 1:
    for i in self.courseList:
        i.config(bg="#ced46a")
    for i in self.cbList:
        i.config(bg="#ced46a")

elif self.checkBg == 2:
    for i in self.courseList:
        i.config(bg="#9cc3d5")
    for i in self.cbList:
        i.config(bg="#9cc3d5")

# if both side(left, right) of space is specified, go down
if self.courseNum % 2 == 0:
    self.newPos += 25
```

#### calculate GPA

```python
i = 0
j = 0
total = 0 # sum of all (grade * 3)
checkCheckedBox = 0 # variable to check whether checkbox checked
self.convertList = [] # list converted letter to number

# get num value from letter
for grades in self.gradeList:
    grades = self.gradeList[i].get()
    self.error = False
    if grades == "A+":
        self.convertList.append(4.33 * 3)
    elif grades == "A":
        self.convertList.append(4.0 * 3)
    elif grades == "A-":
        self.convertList.append(3.67 * 3)
    elif grades == "B+":
        self.convertList.append(3.33 * 3)
    elif grades == "B":
        self.convertList.append(3.0 * 3)
    elif grades == "B-":
        self.convertList.append(2.67 * 3)
    elif grades == "C+":
        self.convertList.append(2.33 * 3)
    elif grades == "C":
        self.convertList.append(2.0 * 3)
    elif grades == "C-":
        self.convertList.append(1.67 * 3)
    elif grades == "D":
        self.convertList.append(1.0 * 3)
    elif grades == "F":
        self.convertList.append(0)
    else:
        showerror("ERROR", "Wrong Input")
        self.error = True
        break
    i += 1

for includes in self.convertList:
    if self.includeList[j].get(): # check elements in convertList is in includeList
        total += self.convertList[j]
        checkCheckedBox += 1 # to calculate how many courses is checked
    j += 1
finalTotal = format((total / (checkCheckedBox * 3)), ',.2f') # round up 2 decimal points
if self.error == False: # if error, shouldn't be displayed
    showinfo("Result", "GPA : " + finalTotal)
```

[my github repo](https://github.com/HenryChung98/gpaCalculator)
