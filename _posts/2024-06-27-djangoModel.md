---
layout: single
title: "Django Model"
categories: note
tags: [django]
author_profile: false
search: true
use_math: true
---

### Setup

check data -> data modeling -> create field -> create / update model -> apply to django

```python
# models.py
class Menu(models.Model):
    name = models.CharField(max_length=50)
    description = models.CharField(max_length=100)
    price = models.IntegerField()
    img = models.CharField(max_length=255)

    # dt_created = models.DateTimeField(verbose_name="Date Created", auto_now_add=True)
    # verbose_name: convert to data readable
    # auto_now_add: usually used for created

    def __str__(self):
        return self.name
```
error_message: validation depending on the key.


```zsh
python manage.py makemigrations
python manage.py migrate
```

migrations are saved in migrations/0001_initial.py.

More commands

```zsh
python manage.py showmigrations
python manage.py sqlmigrate [project-name] [migrations-file-number]
```

#### Field Types

| Field Name    | Description                                                   | Attributes                                                  |
| ------------- | ------------------------------------------------------------- | ----------------------------------------------------------- |
| CharField     | String field with a defined maximum length                    | max_length (maximum number of characters)                   |
| TextField     | String field with no defined maximum length                   |                                                             |
| EmailField    | String field similar to CharField but checks for email format | max_length=254 (default)                                    |
| URLField      | String field similar to CharField but checks for URL format   | max_length=200 (default)                                    |
| BooleanField  | Field with True or False values                               |                                                             |
| IntegerField  | Field for integer values                                      |                                                             |
| FloatField    | Field for floating-point values                               |                                                             |
| DateField     | Field for date values                                         | auto_now (updates on modify), auto_now_add (sets on create) |
| TimeField     | Field for time values                                         | auto_now, auto_now_add                                      |
| DateTimeField | Field for date and time values                                | auto_now, auto_now_add                                      |

### CRUD

#### Create

Execute django shell

```zsh
python manage.py shell
```

Import data table

```zsh
from [app-name].models import Menu
```

Create data

```zsh
Menu.objects.create(name="chicken",
... description="chicken description",
... price=10,
... img="foods/images/chicken.jpg")

<Menu: chicken>
```

#### Read

Import data table

```zsh
from [app-name].models import Menu
```

Read all data in table

```zsh
Menu.objects.all()
```

Read all data detail in table

```zsh
Menu.objects.all().values()
or
Menu.objects.all().values('price')
```

Ascending / Descending order by price

```zsh
Menu.objects.order_by('price')
```

Count number of row

```zsh
rows = Menu.objects.count()
```

Read specific data

##### Filter

It can return more than 2 data.

```zsh
Menu.objects.filter(name__contains="b") # find item contains 'b', case sensetive
Menu.objects.filter(name__icontains="b") # find item contains 'b'

Menu.objects.filter(name__exact="b") # find item 'b', case sensetive
Menu.objects.filter(name__iexact="b") # find item 'b'

Menu.objects.filter(price__range=(1, 15)) # find item with price between 1 and 15

start_date = datetime.date(2023,8,27)
end_date = datetime.date(2024,6,27)
data = Menu.objects.filter(pub_date__range=(start_date,end_date)) # find item published date between 2023-06-27 and 2024-06-27
```

##### Get

It can return only one data. If there are more than 2, gives an error.

```zsh
Menu.objects.get(id=1) # find item with id 1

```

[More info of Field Lookup](https://docs.djangoproject.com/en/2.2/ref/models/querysets/#field-lookups)

#### Update

Need to assign data to a variable

```zsh
data = Menu.objects.get(id=1)
```

and update it

```zsh
data.name = "fried chicken"

# save is required
data.save()
```

#### Delete

Need to assign data to a variable and delete it.

```zsh
data = Menu.objects.get(id=1)
data.delete()
```

#### Code

```python
# urls.py

from django.urls import path
from . import views

urlpatterns = [
    path('menu/<int:pk>/', views.food_detail, name='food-detail'),
    path('menu/', views.index),
]
```

```python
#views.py
from .models import Menu

def index(request):
    today = datetime.today().date()
    context = dict()
    context["date"] = today
    menus = Menu.objects.all()
    context["menus"] = menus
    return render(request, 'foods/index.html', context=context)


def food_detail(request, pk):
    context = dict()
    menu = Menu.objects.get(id=pk)
    context["menu"] = menu

    return render(request, 'foods/detail.html', context=context)
```

{% raw %}

```python
#index.py
{% extends './base.html' %}
{% load static %}

{% block date-block%}
<div>{{date}}</div>
{% endblock date-block%}

{% block food-container%}
  {% for menu in menus %}
    <div class="food">
      <img src={% get_static_prefix %}{{ menu.img }}/>
      <div class="info">
        <h3>{{menu.name}}</h3>
        <p>{{menu.description|linebreaksbr}}</p>
        <a href={% url 'food-detail' food.id %}>view</a>
      </div>
    </div>
  {% endfor %}
{% endblock food-container%}
```

linebreaksbr: a template filter used to convert line breaks in plain text into HTML line break br tags. This is useful when you want to preserve the formatting of text that contains line breaks when rendering it in an HTML template.
{% endraw %}

### Admin tools

First, create an account

```zsh
python manage.py createsuperuser

# enter your info
Username (leave blank to use 'henrychung'):
Email address:
Password:
Password (again):
Superuser created successfully.
```

You can access the administration website via http://127.0.0.1:8000/admin/

You can handle it in admin.py

```python
# admin.py
from django.contrib import admin
from foods.models import Menu
# Register your models here.

admin.site.register(Menu)
```

![des1](/assets/images/2024-06-27-djangoModel/des1.png)

You can do CRUD the database on this page.
