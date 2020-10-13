# Django

## Get django version

```python
import django
django.__version__
```

## Important `django-admin` commands

```bash
django-admin startproject my_project
django-admin startapp my_app
```

## Important `manage.py` commands

```bash
python manage.py createsuperuser
python manage.py shell
python manage.py runserver
```

### Setup database

Make the migrations defined in `models.py`.

```bash
python manage.py migrate
python manage.py makemigrations my_app
python manage.py migrate
```

## Important django shell commands

```python
from my_app import Topic
t = Topic(top_name="Social Network")
t.save()
print(Topic.objects.all())
quit()
```

## Important imports

```python
from django.conf import url, include
```

```python
from django.db import models

class Topic(models.Model):
    top_name = models.CharField(max_length=264, unique=True)

    def __str__(self):
        return self.top_name
```

## Register models in `admin.py`

> You need to create a superuser to use the admin interface

```python
from django.contrib import admin
from my_app.models import Topic,...

admin.site.register(Topic)
admin.site.register(...)
```

## Use `Faker` library to load initial data

> [http://faker.readthedocs.io](Faker documentation)

```bash
pip install Faker
```

```python
import os

os.environment.setdefault('DJANGO_SETTINGS_MODULE', 'my_project.settings')

import django
django.setup()

import random
from my_app.models.import Topic,...
from faker import Faker

fakegen = Faker()

topics = ['Search', 'Social', 'News', ...]

def add_topic():
    t = Topic.object.get_or_create(top_name=random.choice(topics))[0]
    t.save()
    return t

def populate(N=5):
    for entry in range(N):
        # get the topic for the entry
        top = add_topic()
        # create the fake data for that entry
        fake_url = fakegen.url()
        fake_date = fakegen.date()
        fake_name = fakegen.company()
        # create the new webpage entry
        webpg = Webpage.objects.get_or_create(topic=top,url=fake_url,name=fake_name)[0]
        # create a fake access record for that webpage
        acc_rec = AccessRecord.objects.get_or_create(name=webpg,...)

if __name__ == '__main__'
    populate(20)
```

```bash
python populate.py
```

## Authorization related stuff

### Password hashing

```bash
pip install bcrypt
pip install django[argo2]
```

`settings.py`:

> See [Django Documentation](https://docs.djangoproject.com/en/3.1/topics/auth/passwords/#module-django.contrib.auth.password_validation)

```python
PASSWORD_HASHES = [
    'django.contrib.auth.hashers.Argon2PasswordHasher',
    'django.contrib.auth.hashers.PBKDF2PasswordHasher',
]

AUTH_PASSWORD_VALIDATORS = [
    'NAME': '...',
    'OPTIONS': {'min_length': 9}
]
```

### User Models

```python
from django.contrib.auth.models import User

class UserProfileInfo(models.model):
    # Create a relationship to User
    user = models.OneToOneField(User)

    # Add additional fields
    ...
```

## Add image support for python

```bash
pip install pillow
```

## Using `pythonanywhere`

1. Goto [Python Anywhere](https://www.pythonanywhere.com)
2. Create an accont
3. Launch the bash console
4. Create a virtual environment

```bash
mkvirtualenv --python=3.8 myproj
```

5. Install `django`

```bash
pip install -U django==<same_version_you_used_for_your_local_project>
```

> To get `django` version see [Get django version](#get-django-version)

6. Clone the git repo

```bash
git clone ...
```

7. Apply migrations

```bash
python manage.py migrate
python manage.py makemigrations basic_app
python manage.py migrate
```

8. Create a superuser

```bash
python manage.py createsuperuser
```
