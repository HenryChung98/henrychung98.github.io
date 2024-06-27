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

    def __str__(self):
        return self.name
```


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

### CRUD

#### Create

Execute django shell
```zsh
python manage.py shell
```

Import data table
```zsh
from [project-name].models import Menu
```

Create data
```zsh
Menuobjects.create(name="chicken",
... description="chicken description",
... price=10,
... img="foods/images/chicken.jpg")

<Menu: chicken>
```



#### Read
Import data table
```zsh
from [project-name].models import Menu
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