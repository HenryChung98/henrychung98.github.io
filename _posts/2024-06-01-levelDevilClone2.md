---
layout: single
title: "Clone Level Devil_2"
categories: project
tags: [clone-game]
author_profile: false
search: true
use_math: true
---

#### Button class
I am going to create button class to select stage.

```python 
import pygame
from variables import *

class Button:
    def __init__(self, text, x, y, width, height, callback):
        self.text = text
        self.rect = pygame.Rect(x, y, width, height)
        self.color = BLUE  
        self.callback = callback

    def draw(self, screen):
        pygame.draw.rect(screen, self.color, self.rect)
        font = pygame.font.Font(None, 20)
        text_surf = font.render(self.text, True, BLACK) 
        text_rect = text_surf.get_rect(center=self.rect.center)
        screen.blit(text_surf, text_rect)

    def check_click(self, pos):
        if self.rect.collidepoint(pos):
            self.callback()
```
So when button is clicked, function is parameter callback is called.

```python 
# main.py

import pygame
import sys
from variables import *
from button import Button

import stage1

pygame.init()
clock = pygame.time.Clock()
running = True

# button
stage1_btn = Button('Stage 1', 100, 100, 50, 50, stage1.run)

# loop
while running:
    
    screen.fill(BLACK)

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_ESCAPE:
                running = False

        if event.type == pygame.MOUSEBUTTONDOWN:
            stage1_btn.check_click(event.pos)   

    # draw buttons
    stage1_btn.draw(screen)

    pygame.display.flip()
    clock.tick(60) 

pygame.quit()
sys.exit()

```
I created stage1.py file and changed main.py to display button. stage1.py is pretty same as previous main.py. Just made the code to a run() function.


![des1](/assets/images/2024-06-01-levelDevilClone2/des1.png)

#### Detect ground
If there is no any wall object, ground will be SCREEN_HEIGHT. I want to make player can stay on the wall object.

First, need to declare that ground is SCREEN_HEIGHT

```python
ground = SCREEN_HEIGHT
```

And when player's X position is greater than wall's X position and player's X position is less than wall's width, it means player is on the wall.

```python
if player.pos[0] >= wall.pos[0] and player.pos[0] <= wall.w:
            ground = wall.h
else:
    ground = SCREEN_HEIGHT
```

Need to fix update function as well

```python
def update(self, ground):
    if self.is_jump == True:

        if self.v > 0:
            F = (0.5 * self.m * (self.v * self.v))
        else:
            F = -(0.5 * self.m * (self.v * self.v))

        self.pos[1] -= round(F)
        self.v -= 0.2
        if self.pos[1] > ground - self.size:
            self.pos[1] = ground - self.size
            self.is_jump = False
            self.v = VELOCITY
```

![des2](/assets/images/2024-06-01-levelDevilClone2/des2.png)

#### Develop Stages
