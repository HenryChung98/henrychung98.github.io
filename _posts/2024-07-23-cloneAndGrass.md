---
layout: single
title: "Planting Grass after Clone"
categories: project
tags: [django]
author_profile: false
search: true
use_math: true
---

When you clone a project from github and push it, grass is not planted for some reason. 

There is a simple solution.

```zsh
git config --global user.name "Your GitHub Username"
git config --global user.email "your_email@example.com"
```

and check your name and email is set.

```zsh
git config --global user.name
git config --global user.email
```

Now when you push what you cloned, grass will be planted.