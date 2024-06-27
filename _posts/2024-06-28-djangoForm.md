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
<form>{% csrf_token %}
    {{form.as_ul}}
    <input type="submit", value="Submit">
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
