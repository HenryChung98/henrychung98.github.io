---
layout: single
title: "Django URL"
categories: note
tags: [django]
author_profile: false
search: true
use_math: true
---


### Create URL

Go to urls.py in [directory name] import 'include', and add path(app-directory-name, include(app-directory-name.urls)) in urlpatterns list.

```python
from django.contrib import admin
from django.urls import path,include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('[app-directory-name]/', include('[app-directory-name].urls'))
]
```

After, create urls.py in your app's directory and write

```python
from django.urls import path
from . import views

urlpatterns = [
    path('[path-name]/', views.index)
]
```

Go to views.py and add code for index.html.

```python
from django.shortcuts import render

def index(request):
    return render(request, 'foods/index.html')
```

Lastly, create templates/[app] directory in [app] directory and create index file in that.

#### Set Default Page

Once you set the path, when you go to 'http://127.0.0.1:8000/', 404 page will be shown.

To fix this issue,

Add path('', include('app.urls')) in urlpatterns

```python
urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('app.urls')),
]
```

Now this is pointing to app/urls.py file. Go to urls.py in app and you can handle it like

```python
urlpatterns = [
    path('index/', views.index),
    path('', views.index),
]
```

or create your dafault page.


