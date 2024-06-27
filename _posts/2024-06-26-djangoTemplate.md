---
layout: single
title: "Django Template"
categories: note
tags: [django]
author_profile: false
search: true
use_math: true
---

### Static files

Create static/app-name/ in app's directory and these will manage inside of it(css, images, font, etc).

Go to index.html and add

```html
{% load static %}
```

at very top so that this file is using the static files.

After, to get the files like img or css,

```h
<link rel="stylesheet" href={% static 'foods/css/styles.css' %}> <img src={%
static 'foods/images/chicken.jpg' %}/>
```

### Templates

#### Parent Template

```h
<!-- base.html -->
{% load static %}
<!DOCTYPE html>
<html>
  <head>
    <title>Restaurant</title>
    <meta charset="utf-8" />
    <link rel="stylesheet" href={% static 'foods/css/styles.css' %}>
  </head>
  <body>
    <div>{% block date-block %}</div>
    <div>{% endblock date-block %}</div>
    <hr />

    <h1>Restaurant</h1>

    <div class="food-container">
      {% block food-container %} {% endblock food-container %}
    </div>
  </body>
</html>
```

#### Child Template

```h
<!-- index.html -->
{% extends './base.html' %} {% load static %} {% block date-block%}
<div>26 June, 2024</div>
{% endblock date-block%} {% block food-container%}
<div class="food">
  <img src={% static 'foods/images/chicken.jpg' %}/>
  <div class="info"></div>
</div>

<div class="food">
  <img src={% static 'foods/images/sushi.jpg' %}/>
  <div class="info"></div>
</div>

<div class="food">
  <img src={% static 'foods/images/burger.jpg' %}/>
  <div class="info"></div>
</div>

<div class="food">
  <img src={% static 'foods/images/bibimbap.jpg' %}/>
  <div class="info"></div>
</div>

<div class="food">
  <img src={% static 'foods/images/croquette.jpg' %}/>
  <div class="info"></div>
</div>

<div class="food">
  <img src={% static 'foods/images/pumpkin_soup.jpg' %}/>
  <div class="info"></div>
</div>

<div class="food">
  <img src={% static 'foods/images/banana.jpg' %}/>
  <div class="info"></div>
</div>
{% endblock food-container%}
```

### Pass variable to html

```python
# views.py

def index(request):
    today = datetime.today().date()
    contextv = {"date": today} # key: value
    return render(request, 'foods/index.html', context=contextv)
```

```html
<!-- index.html -->

{% block date-block%}
<div>{{date}}</div>
{% endblock date-block%}
```


### Dynamic URL

```python
# urls.py
urlpatterns = [
    path('index/', views.index),
    path('menu/<str:food>/', views.food_detail),
]

```
This 'food' variable can be passed to 
```python
# views.py
def food_detail(request, food):
    context = {"name":food}
    return render(request, 'foods/detail.html', context=context)

```
food parameter here.

Now, create detail.html file in templates and 
```html
<!-- detail.html -->
<h2>{{name}}</h2>
```

![des1](/assets/images/2024-06-26-djangoTemplate/des1.png)

#### Use Static file in Dynamic file
You need {% get_static_prefix%} to use it
```h
<!-- e.g. -->
<img src={% get_static_prefix%}{{img}} />
```

#### 404 page
```python
from django.http import Http404

if food == 'chicken':
    context["name"] = "chicken"
    context["description"] = "chiken des"
    context["price"] = 12
    context["img"] = "foods/images/chicken.jpg"
elif food == 'beef':
    context["name"] = "beef"
.
.
.
else:
    raise Http404("no food")

```
