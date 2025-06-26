---
layout: single
title: "Fixing Missing Commits on GitHub"
categories: git
tags: [minimal-mistakes]
author_profile: false
search: true
use_math: true
---

If you use github, you may know when you commit, the small square will be filled green.

![des1](/assets/images/2024-02-25-plantGrass/des1.png)

This blog was created by forking the Minimal Mistakes theme, but I ran into an issue. Whenever I wanted to update the blog, such as by posting new content, I had to commit to the repository. However, those commits didn’t show up on my GitHub contribution graph — it stayed empty.

I wasn’t sure if this was because the blog was a fork, but I eventually figured out how to fix it.

You need to create a new repository for your blog instead of using the forked one. Before deleting the forked repository, make sure you have a local copy on your computer. Once you've deleted the forked version, push your blog project to the new repository. This way, your contributions will show up properly on your GitHub graph.
