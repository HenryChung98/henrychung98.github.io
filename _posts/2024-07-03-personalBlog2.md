---
layout: single
title: "Personal Blog Project_2"
categories: project
tags: [django]
author_profile: false
search: true
use_math: true
---

### Create View
{% raw %}

Add path for create view.

```python
# urls.py

urlpatterns = [
    path('', views.index, name='index'),
    path('posts/', views.PostListView.as_view(), name='post-list'),
    path('posts/<int:postId>/', views.PostDetailView.as_view(), name='post-detail'),
    path('posts/create/', views.PostCreateView.as_view(), name='post-create'),
]
```


Create a class to render form page.

```python
# views.py

from django.views.generic import CreateView
from .forms import PostForm
from django.urls import reverse

class PostCreateView(CreateView):
    model = Post # create a new 'Post' object based on 'Post'
    form_class = PostForm # get input from user using class
    template_name = 'posts/postForm.html' # render assigned template

    # redirect to 'post-detail' url if an object successfully created
    def get_success_url(self): 
        return reverse('post-detail', kwargs={'postId': self.object.id})
```
Django automatically checks the validation so if there is an problem for post request, get_success_url function is not executed and error message is returned.

reverse function 
```python
# postForm.html

<form method="post">{% csrf_token %}
    <h3>Title</h3>
    <p>{{form.title}}</p>
    {% for error in form.title.errors %}
    <p>{{error}}</p>
    {% endfor %}
    <h3>Content</h3>
    <p>{{form.content}}</p>
    {% for error in form.content.errors %}
    <p>{{error}}</p>
    {% endfor %}
    <input type="submit" value="Create">
</form>
```
csrf_token is required for security. 

[cross site request forgery](https://docs.djangoproject.com/en/5.0/howto/csrf/)

Change href in postList.html for create button. 

```python
# postList.html
<a href={% url 'post-create' %}>create</a>
```

Now when create hyperlink is clicked, moves to form page. 

![des1](/assets/images/2024-07-03-personalBlog2/des1.png)

and it works

![des2](/assets/images/2024-07-03-personalBlog2/des2.png)


#### Form CSS

Modify postForm.html
```html
{% extends './base.html' %}
{% load static %}
{% block css %}
<link rel="stylesheet" href={% static 'posts/css/form.css' %}>
{% endblock css%}

{% block container%}
<form method="post"> {% csrf_token %}
    <h3>Title</h3>
    <p>{{form.title}}</p>
    {% for error in form.title.errors %}
    <p class='error'>{{error}}</p>
    {% endfor %}
    <h3>Content</h3>
    <p>{{form.content}}</p>
    {% for error in form.content.errors %}
    <p class='error'>{{error}}</p>
    {% endfor %}
    <input type="submit" value="Submit">
</form>
{% endblock container%}
```
and design it.

There is a problem. You cannot attach form.title, form.content since django form automatically designate it. Need to modify forms.py.

```python
# forms.py

class PostForm(forms.ModelForm):

    class Meta:
        model = Post
        fields = '__all__'
        widgets = {'title': forms.TextInput(attrs={
            'class': 'title',
            'placeholder': 'this is placeholder'}),
            'content': forms.Textarea(attrs={'placeholder': 'need content'})}
```

[more info](https://docs.djangoproject.com/en/5.0/ref/forms/fields/)

Now you can design the title.
```css
 .title {
    ...
 }
```


### Update View
Add path for update view.
```python
urlpatterns = [
    path('', views.index, name='index'),
    path('posts/', views.PostListView.as_view(), name='post-list'),
    path('posts/<int:postId>/', views.PostDetailView.as_view(), name='post-detail'),
    path('posts/create/', views.PostCreateView.as_view(), name='post-create'),
    path('posts/<int:postId>/edit/', views.PostUpdateView.as_view(), name='post-update'),
]
```

Pretty same as create view.

```python
class PostUpdateView(UpdateView):
    model = Post 
    form_class = PostForm
    template_name = 'posts/postForm.html'
    pk_url_kwarg = 'postId' # keyword argument

    def get_success_url(self):
        return reverse('post-detail', kwargs={'postId': self.object.id})
```


### Delete View

To create delete view, you need post_confirm_delete.html since you are using django internal function and they require it. I roughly made it. But you need csrf token for this as well since form attribute is used.

```html
<p>{{post.title}}</p>
<p>You sure?</p>

<form method="POST">{% csrf_token %}
    <input type="submit" value="delete">
</form>
```

```python
class PostDeleteView(DeleteView):
    model = Post
    template_name = 'posts/post_confirm_delete.html'
    pk_url_kwarg = 'postId'
    context_object_name = 'post'

    def get_success_url(self):
        return reverse('post-list')
```
And I added delete button to test it.

![des4](/assets/images/2024-07-03-personalBlog2/des4.png)

When click the delete button

![des3](/assets/images/2024-07-03-personalBlog2/des3.png)

Once you click the button, the post will be deleted.


{% endraw %}