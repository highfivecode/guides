[Back to Guides](../README.md)
# Django Crash Course Quick Reference

[Django homepage](https://docs.djangoproject.com)  
[Migrations](https://docs.djangoproject.com/en/1.11/topics/migrations/)

### Setup Workspace
  It is *highly* recommended you store all your code in a workspace directory that is easily accessible from the terminal and your computer's graphical interface. A great place is on your desktop or in your home directory. Keep your workspace organized by further breaking it into language specific directories. See the example below for a suggested workspace directory structure.

```
  - Desktop
    - workspace
      - python
        - django
          - djangoproject1
          - djangoproject2
      - java
      - javascript
      - cplusplus
      - venvs
        - djangoproject1-env
        - djangoproject2-env
```

### Activate Your Virtual Environment

See the cheat sheet: [Virtual Environment Cheatsheet](./VirtualEnvCheatSheet.md)

### Install Django or Make Sure Django is Already Installed

Use pip freeze to check.

```shell
$ pip freeze
Django==1.11.6
```

Or launch the python interpreter and import django. 

```shell
$ python
```

```python
>>> import django
>>> django.VERSION
(1, 11, 6, 'final', 0)
>>> quit()
```

If django is not installed, install it using pip. MAKE SURE YOU HAVE ACTIVATED YOUR VIRTUAL ENVIRONMENT!

```shell
(myFirstVirutalEnvironment) $ pip install django
```

To specify a specific django version, use the syntax below:

```shell
(myFirstVirutalEnvironment) $ pip install django==1.10.5
```

### CD Into Where You Want Your Project to Live

```shell
$ cd ~/Desktop/workspace/python/django
```

### Start Your First Project!

```shell
$ django-admin startporject myFirstProject
```

### Migrate your database

Migrations are Django's way of updating your database. We will get more familiar with them later. However right now we need to run a migration to build the initial database that django will use.

```shell
$ python manage.py migrate
```

This command will create a file called db.sqlite3 which is what we will use for our database. See more on migrations [here](https://docs.djangoproject.com/en/1.11/topics/migrations/)

### Launch Your Server

Change directory into your projects root level directory. You will see a file called 'manage.py' there.

``` shell
$ cd myFirstProject
$ python manage.py runserver
```

This starts a lightweight development Web server on the local machine. By default, the server runs on port 8000 on the IP address 127.0.0.1. Open a browser and type in '127.0.0.1:8000' or 'localhost:8000'. You should your first django powered web page!

Press ctrl + c to quit the server.
