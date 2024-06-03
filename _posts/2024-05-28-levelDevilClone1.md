---
layout: single
title: "Clone Level Devil_1"
categories: project
tags: [clone-game]
author_profile: false
search: true
use_math: true
---

### Programming languages used

- python

### Introduction

The Snake Game is a classic and simple video game that has been popular since the early days of computer gaming. The game concept is straightforward: control a snake on a grid or game board, and the snake grows longer as it consumes food. This project is quite helpful for your portfolio.

### prerequisites

```zsh
pip3 install pygame
```

```python
import sys
import pygame
```

[more info pygame](https://www.pygame.org/docs/)

### code

#### initialize

Basic set up code of pygame

```python
import pygame
from player import Player
SCREEN_WIDTH = 1280
SCREEN_HEIGHT = 720

# pygame setup
pygame.init()
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
clock = pygame.time.Clock()
running = True


while running:

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False


    pygame.display.flip()

    clock.tick(60)  # limits FPS to 60

pygame.quit()
```

#### Player class

Create player class

```python
import pygame

class Player:
    def __init__(self, x, y, size):
        self.size = size
        self.pos = [x, y]
        self.dx = 0
        self.dy = 0
        self.texture = pygame.image.load("imgs/player-img.png")
        self.texture = pygame.transform.scale(self.texture, (size, size))

    def draw(self, screen):
        screen.blit(self.texture, self.pos)

    def move_x(self):
        self.pos[0] += self.dx


```

For moving function

```python
    player.move_x()
    for event in pygame.event.get():

        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT:
                player.dx -= 3

            if event.key == pygame.K_RIGHT:
                player.dx += 3


        if event.type == pygame.KEYUP:
            if event.key == pygame.K_LEFT:
                player.dx = 0

            if event.key == pygame.K_RIGHT:
                player.dx = 0

```

when keyup, player stops

#### Jump
I haven't learned physics, so I have no idea how to implement jump function, so I got some code for that from [here](https://www.jbmpa.com/pygame/19)

Player class
```python
import pygame
from variables import *



class Player:
    def __init__(self, x, y, size):

        # physics
        self.is_jump = False
        self.v = VELOCITY
        self.m = MASS


    def jump(self):
        self.is_jump = True

    def update(self):
        if self.is_jump == True:

            if self.v > 0:
                F = (0.5 * self.m * (self.v * self.v))
            else:
                F = -(0.5 * self.m * (self.v * self.v))

            self.pos[1] -= round(F)
            self.v -= 1

            if self.pos[1] > SCREEN_HEIGHT - self.size:
                self.pos[1] = SCREEN_HEIGHT - self.size
                self.is_jump = False
                self.v = VELOCITY


```

Main file
```python
import pygame
import sys
from player import Player
SCREEN_WIDTH = 1280
SCREEN_HEIGHT = 720

# pygame setup
for event in pygame.event.get():
    if event.type == pygame.KEYDOWN:
        if event.key == pygame.K_SPACE:
            player.jump()

    player.update()

```
#### Wall class
```python
import pygame

class Wall:
    def __init__(self, x, y, width, height, color):
        self.pos = [x, y]
        self.w = width
        self.h = height
        self.rect = pygame.Rect(x, y, width, height)
        self.color = color

    def draw(self, screen):
        pygame.draw.rect(screen, self.color, self.rect)
```

```python
# main.py
wall = Wall(SCREEN_WIDTH // 2 + 250, SCREEN_HEIGHT - 30, 100, 20, WHITE)
```

#### Trap class
```python
import pygame

class Trap:
    def __init__(self, x, y, width, height, color):
        self.rect = pygame.Rect(x, y, width, height)
        self.color = color

    def draw(self, screen):
        pygame.draw.rect(screen, self.color, self.rect)
```

```python
# main.py
trap = Trap(SCREEN_WIDTH // 2 + 150, SCREEN_HEIGHT - 30, 20, 20, RED)
```

#### Collision Detection
Pygame offers collision detection function so I can simply make it.

```python
    if player.rect.colliderect(wall.rect):
        wall.color = RED  

    else:
        wall.color = WHITE

    if player.rect.colliderect(trap.rect):
        player.texture = pygame.image.load("imgs/playerDead-img.png")

```
![des1](/assets/images/2024-05-28-levelDevilClone1/des1.png)

![des2](/assets/images/2024-05-28-levelDevilClone1/des2.png)

![des3](/assets/images/2024-05-28-levelDevilClone1/des3.png)