---
layout: single
title: "Snake Game"
categories: project
tags: [python, pygame]
author_profile: false
search: true
use_math: true
---

### introduction

The Snake Game is a classic and simple video game that has been popular since the early days of computer gaming. The game concept is straightforward: control a snake on a grid or game board, and the snake grows longer as it consumes food. This project is quite helpful for your portfolio.

### prerequisites

```bash
pip3 install pygame
```

```python
import pygame
import sys
import copy
import random
import time
```

[more info pygame](https://www.pygame.org/docs/)

### code

#### initialize

This code is basic set up for the game.

```python
pygame.init()

width = 500
height = 500
scale = 10
score = 0

food_x = 10
food_y = 10

display = pygame.display.set_mode((width, height))
pygame.display.set_caption("Snake Game")
clock = pygame.time.Clock() # similar to delta time

def gameLoop():
    running = True

    while running:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                running = False


        # update screen
        pygame.display.flip()

        # 60frames per a second
        clock.tick(60)

gameLoop()
```

And we need 2 classes

- Snake
- Food

#### snake class

```python
class Snake:
    def __init__(self, x_start, y_start):
        self.x = x_start
        self.y = y_start
        self.w = 10
        self.h = 10
        self.x_dir = 1
        self.y_dir = 0
        self.history = [[self.x, self.y]]
        self.length = 1

    def reset(self):
        self.x = width / 2 - scale
        self.y = height / 2 - scale
        self.w = 10
        self.h = 10
        self.x_dir = 1
        self.y_dir = 0
        self.history = [[self.x, self.y]]
        self.length = 1

    def show(self):
        for i in range(self.length):

```

#### food class

```python
class Food:
    def new_location(self):
        global food_x, food_y
```
