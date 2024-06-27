---
layout: single
title: "Django Deploy"
categories: note
tags: [django]
author_profile: false
search: true
use_math: true
---

### Prepare to Deploy
Before you deploy, you must turn off debug mode. Otherwise, it leads to security issues.

Go to settings.py and change DEBUG = True to False and add your deploy website to in ALLOWED_HOSTS.
```python
DEBUG = False
ALLOWED_HOSTS = ['.pythonanywhere.com']
```
Lastly, all static files should be in one directory. Add this line at very bottom in setting.py
```python
STATIC_ROOT = os.path.join(BASE_DIR, 'static')
```

And write 
```zsh
python manage.py collectstatic
```

### Deploy(pythonanywhere)
1. zip your project directory

2. Go to pythonanywhere website

3. Click 'Files' and upload your zipfile

4. Click Open Bash console

5. Make sure your file is uploaded

6. 
```zsh
upzip [file.zip]

virtualenv --python=python[version] django-envs

cd django-envs

source bin/activate

pip install django==2.2
```
7. Go to webpage and Click 'Add a new web app'.

8. Click 'Manual configuration'

9. Select python version that you chose when you create virtual environment.

10. Modify 'Source code' in 'Code' section to /home/[your id]/[project]. There is your id below it(Working dirctory: /home/[your id]).

11. Click WSGI configuration file and comment 19th line to 47th line.

12. Uncomment 76th line to 89th line.

13. Modify 81st line to '/home/[your id]/[project].

14. Modify 85th line to 'os.environ['DJANGO_SETTINGS_MODULE'] = '[project].settings'.

15. Save it and move to 'web'.

16. Set 'Virtualenv' section. Add '/home/[your id]/django-envs.

17. Set 'Static files' section. URL to '/static/ and Directory to '/home/[your id]/[project]/static'

18. Go to the top and Click Reload and you will see your website link.
