---
layout: single
title: "Vim Commands"
categories: commands
tags: [Vim]
author_profile: false
search: true
---

### Execute

```zsh
vim
```

or

```zsh
vim path/to/file
```

### Commands

| Function                | Mode                 | Description                                |
| ----------------------- | -------------------- | ------------------------------------------ |
| Text Input              | Insert Mode (i)      | Enter text                                 |
| Copy a Line of Text     | Normal Mode          | Place cursor on the line to copy → `yy`    |
| Cut a Line of Text      | Normal Mode          | Place cursor on the line to cut → `dd`     |
| Copy a Specific Area    | Visual Mode (v or V) | Select the area with the cursor → `y`      |
| Cut a Specific Area     | Visual Mode (v or V) | Select the area with the cursor → `d`      |
| Paste Text              | Normal Mode          | Place cursor where you want to paste → `p` |
| Save File               | Command Mode (:)     | `w [file_name.txt]` + enter                |
| Save File + Exit vim    | Command Mode (:)     | `wq` + enter                               |
| Exit vim Without Saving | Command Mode (:)     | `q!` + enter                               |
