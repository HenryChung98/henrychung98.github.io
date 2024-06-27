---
layout: single
title: "Django Structure"
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

### URL

#### Create URL

1. Go to urls.py in [directory name]

You will see a default code.

```python
from django.contrib import admin
from django.urls import path

urlpatterns = [
    path('admin/', admin.site.urls),
]
```

2. Add 'include behind path and add a path with parameter (app-directory-name, include(app-directory-name.urls))

```python
from django.contrib import admin
from django.urls import path,include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('[app-directory-name]/', include('[app-directory-name].urls'))
]
```

3. Create urls.py in your app's directory and write

```python
from django.urls import path
from . import views

urlpatterns = [
    path('index/', views.index)
]
```

4. Go to views.py and add code for index html.

```python
from django.http import HttpResponse

def index(request):
    return render(request, 'foods/index.html')
```

##### Template(HTML)

Generally create templates directory in app's directory and create app's directory again in templates directory and create HTML file in that.
project
└── project
└── app
    └── templates
        └── app   <!-- django directory structure -->
            └── index.html

```html
<h2>Hello django</h2>
<p> hello</p>
```

After you run the server, you see the index page at 'http://127.0.0.1:8000/app-directory-name/index

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


