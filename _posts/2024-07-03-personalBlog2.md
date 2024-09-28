---
layout: single
title: "Personal Blog Project_2"
categories: project
tags: [django]
author_profile: false
search: true
use_math: true
---

[Personal Blog Project_1](https://henrychung98.github.io/project/personalBlog1/)
[Personal Blog Project_3](https://henrychung98.github.io/project/personalBlog3/)

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
{% extends './base.html' %} {% load static %} {% block css %} <link
rel="stylesheet" href={% static 'posts/css/form.css' %}> {% endblock css%} {%
block container%}
<form method="post">
  {% csrf_token %}
  <h3>Title</h3>
  <p>{{form.title}}</p>
  {% for error in form.title.errors %}
  <p class="error">{{error}}</p>
  {% endfor %}
  <h3>Content</h3>
  <p>{{form.content}}</p>
  {% for error in form.content.errors %}
  <p class="error">{{error}}</p>
  {% endfor %}
  <input type="submit" value="Submit" />
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
  ...;
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

<form method="POST">
  {% csrf_token %}
  <input type="submit" value="delete" />
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

##### Learned New

###### Seeding

Seeding is the process of populating the database with initial or sample data

Seeding is the process of populating the database with initial or sample data

There is a package that can create a bunch of dump data.

```zsh
pip install django-seed
```

and add django_seed in INSTALLED_APPS in settings.py

```python
# settings.py
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'posts',
    'django_seed'
]
```

Now you can create data.

```zsh
python manage.py seed posts --number=[number of data]
```

![des6](/assets/images/2024-07-03-personalBlog2/des6.png)

Or you can add data manually.

First, create a data with title: title_data_01 and content: content_data_01.
![des5](/assets/images/2024-07-03-personalBlog2/des5.png)

After, create json file.

```zsh
python manage.py dumpdata posts --indent=2 > posts_data.json
```

I got this json file. you can copy and paste this data and change pk.

```json
[
  {
    "model": "posts.post",
    "pk": 3,
    "fields": {
      "title": "title_data_01",
      "content": "content_data_01",
      "createdAt": "2024-07-04T05:57:31.075Z",
      "modifiedAt": "2024-07-04T05:57:31.075Z"
    }
  }
]
```

Then apply the data to the app.

```zsh
python manage.py loaddata posts_data.json
```

###### Pagination

Execute shell

```zsh
python manage.py shell
```

Import Paginator function from django and Post from database model.

```zsh
from django.core.paginator import Paginator
from posts.models import Post
```

Assign all objects of Post database to a variable and create pages which has 10 objects each.

```zsh
posts = Post.objects.all()
pages = Paginator(posts, 10)
```

More Functions 

| Method & Attribute              | Description                                   | Example                         |
| ------------------------------- | --------------------------------------------- | ------------------------------- |
| `{paginator}.count`             | Number of items in the paginator              | `{paginator}.count`             |
| `{paginator}.num_pages`         | Total number of pages in the paginator        | `{paginator}.num_pages`         |
| `{paginator}.page_range`        | Range of pages in the paginator               | `{paginator}.page_range`        |
| `{paginator}.page(num)`         | Page object for the specified page number     | `{paginator}.page(1)`           |
| `{page}.has_next()`             | Whether the page has a next page              | `{page}.has_next()`             |
| `{page}.has_previous()`         | Whether the page has a previous page          | `{page}.has_previous()`         |
| `{page}.has_other_pages()`      | Whether the page has other pages              | `{page}.has_other_pages()`      |
| `{page}.number`                 | Current page number                           | `{page}.number`                 |
| `{page}.object_list`            | List of objects on the page                   | `{page}.object_list`            |
| `{page}.paginator`              | Paginator of the page                         | `{page}.paginator`              |
| `{page}.next_page_number()`     | Number of the next page                       | `{page}.next_page_number()`     |
| `{page}.previous_page_number()` | Number of the previous page                   | `{page}.previous_page_number()` |
| `{page}.start_index()`          | Index of the first item on the page (1-based) | `{page}.start_index()`          |
| `{page}.end_index()`            | Index of the last item on the page (1-based)  | `{page}.end_index()`            |


After, modify postList template and in postList class views.py.

```python
class PostListView(ListView):
    model = Post
    template_name = 'posts/postList.html'
    context_object_name = 'posts'
    ordering = ['-createdAt']
    paginate_by = 10
    page_kwarg = 'page'
```

```html
{% extends './base.html' %} 
{% load static %} 
{% block css%}
<link rel="stylesheet" href={% static 'posts/css/style.css' %}>
{% endblock css%}
{% block header %}
<h1>Personal Blog</h1>
<a href={% url 'post-create' %}>create</a>
{% endblock header %} 

{% block container%} 
{% if page_obj.object_list %}
<table>
  <tr>
      <th>Title</th>
      <th>Updated</th>
  </tr>
{% for post in page_obj.object_list %}
        <tr>
            <td><a href={% url 'post-detail' post.id %}>{{post.title}}</a></td>
            {% if post.modifiedAt.day == today.day %}
            <td>{{post.modifiedAt|time:"H:i"}}</td>
            {% else %}
            <td>{{post.modifiedAt.month}} / {{post.modifiedAt.day}}</td>
            {% endif%}
        </tr>
        {% endfor%}
      </table>
      <div class="paginator">
        {% if page_obj.has_previous %}
          <a href="?page=1" class="first">first</a>
          <a href="?page={{ page_obj.previous_page_number }}" class="prev">prev</a>
        {% endif %}
        
        <span>
          <p>{{page_obj.number}} of {{page_obj.paginator.num_pages}}</p>
        </span>

        {% if page_obj.has_next %}
          <a href="?page={{page_obj.next_page_number}}" class="next">next</a>
          <a href="?page={{page_obj.paginator.num_pages}}" class="last">last</a>
        {% endif %}

      </div>
{% else %}
<div class="blank">
  <p>No Content</p>
</div>
{% endif %} {% endblock container%}
```
{% endraw %}
