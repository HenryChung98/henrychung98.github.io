---
layout: single
title: "Push Unreal Engine Project to Github"
categories: note
tags: [unrealEngine]
author_profile: false
search: true
use_math: true
---

#### Install and Setting

Install [Git Large File Storge(LFS)](https://git-lfs.com/)

```zsh
git lfs install
```

Specify the file type to manage

```zsh
git lfs track "*.uasset"
git lfs track "*.umap"
git lfs track "*.png"
git lfs track "*.jpg"
git lfs track "*.wav"
git lfs track "*.mp4"
```

#### Push 

```zsh
git add .gitattributes
git add .
git commit -m "Set up Git LFS for Unreal Engine"
git lfs push --all origin main
git push origin main 
```

Check LFS is set

```zsh
git lfs ls-files
```

#### Pull or Clone
```zsh
git clone https://your-repo-url.git
git lfs pull
```


#### Trouble Shooting

Fix Git LFS objects missing

```zsh
git lfs fetch --all
git lfs pull
```


If .gitattributes file is gone

```zsh
git lfs track "*.uasset"
git add .gitattributes
git commit -m "Fix Git LFS tracking"
git push origin main
```