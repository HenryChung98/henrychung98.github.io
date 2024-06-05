---
layout: single
title: "Clone Level Devil_3"
categories: project
tags: [clone-game]
author_profile: false
search: true
use_math: true
---

#### Check Opened Stages

```python
opened_stages = []

try:
    with open('opened-stages.txt', 'r') as file:
        lines = file.readlines()
        for line in lines:
            check_num = []
            for i in line:
                try:
                    if int(i):
                        check_num.append(i)
                except:
                    continue
            
            combined = ""
            for i in check_num:
                combined += i

            opened_stages.append(int(combined))

except:
    with open('opened-stages.txt', 'w') as file:
        file.write("1\n")
```
I made an algorithm to check opened stages.

if there is no 'opened-stages.txt' file, it means a user has never played this game, so create 'opened-stages.txt' file and write 1. Else, read the file. 

There is '\n' string, but I need to read just number so 
```python
for line in lines:
    check_num = []
    for i in line:
        try:
            if int(i):
                check_num.append(i)
        except:
            continue
```

this code filters '\n', and append numbers to temporary list.

```python
    combined = ""
    for i in check_num:
        combined += i

    opened_stages.append(int(combined))
```

This code combined a list to a value and append this value to opened_stages list.

After, I modified code for creating buttons.

```python
stage_btns = []
button_details = {
    1: ('Stage 1', 100, 100, 50, 50, stage1_1.run),
    2: ('Stage 2', 200, 100, 50, 50, stage1_2.run),
    3: ('Stage 3', 300, 100, 50, 50, stage1_3.run)
}

for stage in opened_stages:
    if stage in button_details:
        label, x, y, width, height, action = button_details[stage]
        stage_btns.append(Button(label, x, y, width, height, action))
```

Lastly, I added this code to each stage files except first stage so that if this stage is executed, append the stage number to opened-stages file and now you see the button for the stage.

```python
# stage 2
    with open('opened-stages.txt', 'r') as file:
        lines = file.readlines()
        is_opened = False
        for line in lines:
            if line == "2\n":
                is_opened = True
                break
        
        if is_opened == False:
            with open('opened-stages.txt', 'a') as file:
                file.write("2\n")

```

![des1](/assets/images/2024-06-05-levelDevilClone3/des1.png)
![des2](/assets/images/2024-06-05-levelDevilClone3/des2.png)
![des3](/assets/images/2024-06-05-levelDevilClone3/des3.png)
![des4](/assets/images/2024-06-05-levelDevilClone3/des4.png)


##### Learned New

I added 3 arrow key images to explain how to play briefly. 

```python
arrow_up = pygame.image.load("imgs/up-arrow.png")
arrow_right = pygame.image.load("imgs/right-arrow.png")
arrow_left = pygame.image.load("imgs/left-arrow.png")

.
.
.
screen.blit(arrow_up, (SCREEN_WIDTH / 2 - 32, SCREEN_HEIGHT / 4 * 3 - 64))
screen.blit(arrow_left, (SCREEN_WIDTH / 2 - 96, SCREEN_HEIGHT / 4 * 3))
screen.blit(arrow_right, (SCREEN_WIDTH / 2 + 32, SCREEN_HEIGHT / 4 * 3))
```

They are located on a wall, but if those codes are written after

```python
for wall in walls:
    wall.draw(screen)
```

this code, they are not shown because they are drawn first and wall is drawn so they are covered on the wall. So it should be

```python 
screen.blit(arrow_up, (SCREEN_WIDTH / 2 - 32, SCREEN_HEIGHT / 4 * 3 - 64))
screen.blit(arrow_left, (SCREEN_WIDTH / 2 - 96, SCREEN_HEIGHT / 4 * 3))
screen.blit(arrow_right, (SCREEN_WIDTH / 2 + 32, SCREEN_HEIGHT / 4 * 3))

for wall in walls:
    wall.draw(screen)
```


![des5](/assets/images/2024-06-05-levelDevilClone3/des5.png)