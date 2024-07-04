---
layout: single
title: "Django Form"
categories: note
tags: [django]
author_profile: false
search: true
use_math: true
---

### Form

```python
# forms.py

from django import forms

class PostForm(forms.Form):
    title = forms.CharField(max_length=50, label="title")
    content = forms.CharField(label="content", widget=forms.Textarea)

```

or you can refer to the model that you made before

```python
from .models import Menu

class PostForm(forms.ModelForm):

    class Meta:
        model = Menu
        fields = '__all__' # ['name', 'description', 'price', 'img']
```

[More info of Form Field](https://docs.djangoproject.com/en/2.2/ref/forms/fields/#core-field-arguments)

```python
# views.py

from django.shortcuts import render, redirect
from .forms import PostForm

def post_create(request):
    if request.method == 'POST':
        post_form = PostForm(request.POST)

        if post_form.is_valid():
            new_post = post_form.save()
            return redirect('post-detail', post_id = new_post.id)

    else:
        post_form = PostForm()

    return render(request, 'posts/post_form.html', {'form': post_form})
```

{% raw %}

```html
<!-- post_form.html -->
<form>
  {% csrf_token %} {{form.as_ul}}
  <input type="submit" , value="Submit" />
</form>
```

csrf_token: security system offered by django
{% endraw %}

### Validation

You can simply use internal validators. This is to check whether title is duplicated or not.

```python
#models.py

class Post(models.Model):
    title = models.CharField(max_length=50, error_message={'unique': 'Cannot be duplicated'})
```

or you can import external validators.

```python
#models.py

from django.core.validators import MinLengthValidator

class Post(models.Model):
    content =  models.TextField(validators=[MinLengthValidator(10, 'minimum length is 10')])
```

[More info of validators](https://docs.djangoproject.com/en/5.0/ref/validators/)

Also you can create validation function.

```python
#validators.py

from django.core.exceptions import ValidationError

def validate_symbols(value):
    if("@" in value) or ("#" in value):
        raise ValidationError('"@" or "#" cannot be included', code = 'symbol-err')
```

```python
# models.py

from .validators import validate_symbols

class Post(models.Model):
    content =  models.TextField(validators=[MinLengthValidator(10, 'minimum length is 10'), validate_symbols])
```

You can also create a validate function in PostForm class and handle it.

```python
# forms.py

from django import forms
from .models import Post
from .validators import validate_symbols
from django.core.exceptions import ValidationError

class PostForm(forms.ModelForm):


    class Meta:
        model = Post
        fields = '__all__'

    def clean_title(self):
        title = self.cleaned_data['title']
        if '*' in title:
            raise ValidationError('* cannot be included')

        return title

```

### Form HTML

{% raw %}

```html
{% extends './base.html' %}
{% load static %}

{% block css%}
    <link rel="stylesheet" href="{% static 'posts/css/form.css' %}" >
{% endblock css%}

{% block content %}
<form method="post">{% csrf_token %}
    <h3>Title</h3>
    <p class="error">{{form.title}}</p>
    {% for error in form.title.errors %}
    <p class="error">{{error}}</p>
    {% endfor %}
    <h3>Content</h3>
    <p class="error">{{form.content}}</p>
    {% for error in form.content.errors %}
    <p class="error">{{error}}</p>
    {% endfor %}
    <input type="submit", value="Submit">
</form>
{% endblock content %}
```

{% endraw %}


### Post Update

```python
def post_update(request, post_id):
    post = Post.objects.get(id=post_id)

    if request.method == 'POST':
        post_form = PostForm(request.POST, instance=post)
        if post_form.is_valid():
            post_form.save()
            return redirect('post-detail', post_id = post.id)
        
    else:
        post_form = PostForm(instance=post)

    return render(request, 'posts/post_form.html', {'form': post_form})
```


### Post Delete

```python
def post_delete(request, post_id):
    post = Post.objects.get(id=post_id)
    post.delete()
    return redirect('post-list')
```


##### Learned New

You can make view function to class

```python
# function

def post_create(request):
    if request.method == 'POST':
        post_form = PostForm(request.POST)

        if post_form.is_valid():
            new_post = post_form.save()
            return redirect('post-detail', post_id = new_post.id)

    else:
        post_form = PostForm()

    return render(request, 'posts/post_form.html', {'form': post_form})

# url
path('posts/new', views.post_create, name='post-create')
```

```python
# class

from django.views.generic import CreateView

class PostCreateView(CreateView):
    model = Post
    form_class = PostForm
    template_name = 'posts/post_form.html'

    def get_success_url(self):
        return reverse('post-detail', kwargs={'post_id': self.object.id})


# url
path('posts/new', views.PostCreateView.as_view(), name='post-create')
```