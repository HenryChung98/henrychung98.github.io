---
layout: single
title: "Personal Blog Project_3"
categories: project
tags: [django]
author_profile: false
search: true
use_math: true
---

### Validator

#### Use Internal django Validator

```python
# models.py

from django.core.validators import MinLengthValidator

class Post(models.Model):

    content = models.TextField(validators=[MinLengthValidator(10, 'need at least 10 letters.')])

```

#### Create Validator Function

```python
# validators.py

from django.core.exceptions import ValidationError

def validateSymbols(value):
    if ('&' in value):
        raise ValidationError('"&" cannot be included')

```
and need to apply this function in models.py

```python
from .validators import validateSymbols

class Post(models.Model):
    content = models.TextField(validators=[MinLengthValidator(10, 'need at least 10 letters.'), validateSymbols])
```

#### Use Validator at Form

```python
from django.core.exceptions import ValidationError

class PostForm(forms.ModelForm):

    class Meta:
        model = Post
        fields = '__all__'
        widgets = {'title': forms.TextInput(attrs={
            'class': 'title',
            'placeholder': 'this is placeholder'}),
            'content': forms.Textarea(attrs={'placeholder': 'need content'})}
    
    def clean_title(self):
        title = self.cleaned_data['title']
        if '*' in title:
            raise ValidationError('* cannot be included')
        return title

```

![des1](/assets/images/2024-07-04-personalBlog3/des1.png)

[more info about django validator](https://docs.djangoproject.com/en/5.0/ref/validators/)