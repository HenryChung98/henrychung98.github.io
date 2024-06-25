---
layout: single
title: "Django things"
categories: note
tags: [django]
author_profile: false
search: true
use_math: true
---

### App

#### Create App

Move to root directory and

```zsh
python manage.py startapp [app-directory-name]
```

After, you need to register your app in setting.py.

Go to settings.py file and add 'app-directory-name' in INSTALLED-APPS list.