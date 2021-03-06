[Back to Guides](../README.md)
# Django Crash Course Quick Reference

##### Django Documentation References
[Django Homepage](https://docs.djangoproject.com)  
  
[Admin Site](https://docs.djangoproject.com/en/1.11/ref/contrib/admin/)  
[Admin Site Actions](https://docs.djangoproject.com/en/1.11/ref/contrib/admin/actions/)  
[Django Packages](https://djangopackages.org/)     
[Making Queries](https://docs.djangoproject.com/en/1.11/topics/db/queries/)  
[Managers (Querysets)](https://docs.djangoproject.com/en/1.11/topics/db/managers/)  
[Migrations](https://docs.djangoproject.com/en/1.11/topics/migrations/)  
[Model Fields](https://docs.djangoproject.com/en/1.11/ref/models/fields/)  
[Model Forms](https://docs.djangoproject.com/en/1.11/topics/forms/modelforms/)  
[QuerySets](https://docs.djangoproject.com/en/1.11/ref/models/querysets/)  
[QuerySet API](https://docs.djangoproject.com/en/1.11/ref/models/querysets)  
[Templates](https://docs.djangoproject.com/en/1.11/topics/templates/)  
[Template Language](https://docs.djangoproject.com/en/1.11/topics/templates/#the-django-template-language)
  * [Templating Tags Reference](https://docs.djangoproject.com/en/1.11/ref/templates/builtins/#ref-templates-builtins-tags)
  * [Templating Filter Reference](https://docs.djangoproject.com/en/1.11/ref/templates/builtins/#ref-templates-builtins-filters)
  
[Testing In Django](https://docs.djangoproject.com/en/1.11/topics/testing/)  
[Unit Testing In Python](https://docs.python.org/3/library/unittest.html)  
[Working With Forms](https://docs.djangoproject.com/en/1.11/topics/forms/#working-with-form-templates)  
[URL Dispatcher](https://docs.djangoproject.com/en/1.11/topics/http/urls/)  

## Table Of Contents

1. [Workspace Setup](#workspace-setup)
2. [Activate Your Virtual Environment](#activate-your-virtual-environment)
3. [Start Your First Project](#start-your-first-project)
4. [Create a Super User and Log In to the Admin Panel](#create-a-super-user-and-log-in-to-the-admin-panel)
5. [Create a home page](#create-a-home-page)
6. [Django Templating Language](#django-templating-language)
7. [Static Files](#configuring-static-files)
8. [Creating An App](#creating-an-app)
9. [Creating A Model](#creating-a-model)
10. [Making Database Queries](#making-database-queries)
11. [Using Querysets In Templates](#using-querysets-in-templates)  
12. [Creating A Base Template](#creating-a-base-template)  
13. [Models and Many-To-One Relationships](#models-and-many-to-one-relationships)
14. [The Django Admin Panel](#the-django-admin-panel)  
15. [Admin Panel Options](#admin-panel-options)  
16. [Admin Panel Actions](#admin-panel-actions)  
17. [Creating A Form](#creating-a-form)  
18. [Model Forms](#model-forms)  
19. [Dynamic Url Parameters and Editing ModelForms](#dynamic-url-parameters-and-editing-modelforms)  
20. [Using A View To Delete An Object](#using-a-view-to-delete-an-object)  
21. [Using Named Urls In Views](#using-named-urls-in-views)  
22. [Introduction To Automated Testing](#introduction-to-automated-testing)  

### Workspace Setup 
[back to top](#django-crash-course-quick-reference)  
[watch video](https://youtu.be/fGGDw5yRRXE)

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
[back to top](#django-crash-course-quick-reference)  
[watch video](https://youtu.be/fGGDw5yRRXE)

See the cheat sheet: [Virtual Environment Cheatsheet](./VirtualEnvCheatSheet.md)

### Install Django or Make Sure Django is Already Installed
[back to top](#django-crash-course-quick-reference)
[watch video](https://youtu.be/fGGDw5yRRXE)

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


### Start Your First Project!
[back to top](#django-crash-course-quick-reference)  
[watch video](https://youtu.be/fGGDw5yRRXE)

First CD into where you want your project to live:

```shell
$ cd ~/Desktop/workspace/python/django
```

Then run the startproject command

```shell
$ django-admin startproject myFirstProject
```

### Migrate your database
[back to top](#django-crash-course-quick-reference)  
[watch video](https://youtu.be/fGGDw5yRRXE)

Migrations are Django's way of updating your database. We will get more familiar with them later. However right now we need to run a migration to build the initial database that django will use.

```shell
$ python manage.py migrate
```

This command will create a file called db.sqlite3 which is what we will use for our database. See more on migrations [here](https://docs.djangoproject.com/en/1.11/topics/migrations/).

### Launch Your Server
[back to top](#django-crash-course-quick-reference)  
[watch video](https://youtu.be/fGGDw5yRRXE)

Change directory into your projects root level directory. You will see a file called 'manage.py' there.

``` shell
$ cd myFirstProject
$ python manage.py runserver
```

This starts a lightweight development Web server on the local machine. By default, the server runs on port 8000 on the IP address 127.0.0.1. Open a browser and type in '127.0.0.1:8000' or 'localhost:8000'. You should your first django powered web page!

Press ctrl + c to quit the server.

### Create a Super User and Log In to the Admin Panel
[back to top](#django-crash-course-quick-reference)  
[watch video](https://youtu.be/89pwzSE5c0Q)

Super users are users who are granted all privileges by default. They can create, read (view), update, or delete any entries from the database by using the admin panel. Creating them is done through manage.py and uses the createsuperuser command.

```shell
$ python manage.py createsuperuser
```

You will be prompted for a username, email (optional), and password. Once the super user is created you can visit the admin panel by visiting '127.0.0.1:8000/admin' in your web browser. If you decided to run your server on a different port than the default 8000, make sure your url reflects that.

### Create a home page
[back to top](#django-crash-course-quick-reference)  
[watch video](https://youtu.be/Q_Q9umYQzf0)  

Create a new file file in your projects package (the same directory the settings.py is in) called views.py. It should look like the following:

**views.py**
```python
from django.http import HttpResponse

def home(request):
    return HttpResponse('Welcome to our first django app! Powered by Python and the Django Crash Course.')
```

Open your projects root_urlconf file (normally the urls.py file in the project package, which is the same directory the settings.py is in).

Add a new url to the url patterns matching with the first argument set to the string you wish the url to be. Make sure to import views as well, see below.

**urls.py**
```python
from django.conf.urls import url
from django.contrib import admin

from . import views

urlpatterns = [
    url(r'^$', views.home, name='home'), #maps an empty url string such as 'localhost:8000' to the home function in the views file
    url(r'^admin/', admin.site.urls),
]
```

Launch your server, navigate your browser to 'localhost:8000' and see the text from the home function displayed!

### Create a template
[back to top](#django-crash-course-quick-reference)  
[watch video](https://youtu.be/Y2s6qj0kfOA)

Templates allow us to minimize our code for new pages (by extending or inheriting from other templates) and also use template code and template variables passed from the views.

In your root level directory (where manage.py is), create a new directory (use mkdir from the terminal) and call it templates. In templates, create a new bare bones HTML5 like so:

**home.html**
```html
<!DOCTYPE html>
<html>
  <head>
    <title>uStudy</title>
  </head>
  <body>
    <div id="container">
      <h1>Welcome to uStudy!</h1>
    </div>
  </body>
</html>
```

In settings.py, on line 59, change the value of the 'DIRS' keyword from [] to:
```python
'DIRS': [os.path.join(BASE_DIR, 'templates')], #base_dir/templates
```

Finally, change your previous Home view to the following:

**views.py**
```python
from django.shortcuts import render

def home(request):
    '''
    Renders home page
    '''
    context = {} #an empty dictionary
    return render(request, 'home.html', context)
```

### Django Templating Language
[back to top](#django-crash-course-quick-reference)  
[watch video for template variables and filters](https://https://youtu.be/K1pE0sh31Rs)  
[watch video for template tags](https://youtu.be/zZsL-aSXNPw)


Let's replace the the "Welcome to uStudy" H1 tag in the previous template with a template variable. This can be done using django's [templating language](https://docs.djangoproject.com/en/1.11/topics/templates/#the-django-template-language).

```html
<h1>Welcome to uStudy</h1>
```

becomes....

**home.html**
```html
<h1>{{ our_greeting }}</h1>
```

And the greeting variable is declared in the view (the home function in the views.py in this case) and passed to the template using the context, like so:


```python views.py
from django.shortcuts import render

def home(request):
    '''
    Renders home page
    '''
    greeting = "uStudy - the best study site in the world!"
    today = 'tuesday'
    # a dictionary with a keyword 'our_greeting' mapping to the variable greeting defined above.
    context = {'our_greeting':greeting}
    return render(request, 'home.html', context)
```

Filters transform the values of variables and tag arguments, they use a "pipe" | with the variable on the left side of the pipe and the transformation argument on the right side of the pipe. Let's transform our greeting to titlecase, where the first letter of each word is capitalized.

**home.html**
```html
<h1>{{ our_greeting | title }}</h1>
```

Template tags allow us to control logic in the rendering process of the template. Here are a few example of where this is handy:
  * Displaying a greeting only if a user is logged in
  * Displaying a link to the admin panel if the user is a member of the staff
  * Iterating over a list of items
  * Extending templates so we don't need to rewrite all our HTML for every template
  * Using csrf tokens with our forms to protect our site from cross site request forgery attacks.
  
Template tags end and close with a curly brace and a percentage sign: {% %}

A common use is to check if a list exists and either display the list or display an error message if the list does not exists. Let's do this below.

**views.py**
```python views.py
from django.shortcuts import render

def home(request):
    '''
    Renders home page
    '''
    greeting = "uStudy - the best study site in the world!"
    #first we will create a variable with the days of the week as a list
    days_of_week = ['monday', 'tuesday', 'wednesday', 'thursday', 'friday', 'saturday', 'sunday']
    #then we will add it to the template context
    context = {'our_greeting':greeting, 'weekday_list':days_of_week}
    return render(request, 'home.html', context)
```

Now in the home.html template we will add template tags to 1. Check if the list exists and then 2. Iterate over the list
**home.html**
```html
<!DOCTYPE html>
<html>
  <head>
    <title>uStudy</title>
  </head>
  <body>
    <div id="container">
      <h1>Welcome to {{ our_greeting | title }}!</h1>
      {% if weekday_list %}
        <ul>
          {% for day in weekday_list %}
            <li>{{ day|slice:":3" }}</li>
          {% endfor %}
        </ul>
      {% else %}
        <p>Days of week is not defined.</p>
      {% endif %}
    </div>
  </body>
</html>
```

### Configuring Static Files
[back to top](#django-crash-course-quick-reference)  
[watch video](https://youtu.be/daYncgqTg68)

Websites generally need to serve additional files such as images, JavaScript, or CSS. In Django, we refer to these files as “static files”. (Yes, we copied that right from the [static files documentation](https://docs.djangoproject.com/en/1.11/howto/static-files/)). We are gonna to practice using static files by adding an external style sheet to our app.

The process is rather simple:
  1. Make sure that django.contrib.staticfiles is included in your INSTALLED_APPS (it should be by default).
  2. In your settings file, define STATIC_URL, for example:
    * This should be done by default as well. Check the bottom of your settings.py
  ```python
  STATIC_URL = '/static/'
  ```
  3. Much like we did with the templates, we need to tell django where to look for our static files. This is done using the STATICFILES_DIRS variable.
  ```python
  STATICFILES_DIRS = [
    os.path.join(BASE_DIR, "static"),
]
  ```
  4. Now that django is going to look for a folder static in our BASE_DIR (remember, that is the directory where manage.py is), we need to create that folder.
  ```shell
  $ cd /path/to/base/dir
  $ mkdir static
  ```
  5. Now create a new css file inside the static directory and define some css styles.
  6. Finally, in the home.html template we need to link to that using the static tag. The source of the file in the static tag should be RELATIVE to the directory you may in the STATICFILES_DIRS variable. So if you have a file: djangocc/static/style.css you would do the below:
  **home.py**
  ```html
   <head>
    <title>uStudy</title>
    <link rel='stylesheet' href="{% static 'style.css' %}" />
  </head>
 ```
 
 However we like to organize our static folders a bit better and add additional directories for css, javascript, and images inside of it. To like to a file in djangocc/static/css/style.css the correct tag would be:
 
 ```html
<link rel='stylesheet' href="{% static 'css/style.css' %}" />
```
 
  
> IMPORTANT: The settings above are for LOCAL development only. They will work fine for our tutorial project but do not attempt to deploy your application live using these settings.
> For more information, look at the django docs and the [deploying static files docs](https://docs.djangoproject.com/en/1.11/howto/static-files/deployment/)

### Creating an App
[back to top](#django-crash-course-quick-reference)  
[watch video](https://youtu.be/UTaFD-OlCEk)


We already created a django project, now we will create an app. The terminology is confusing so lets define each:

1. Django project - a web application powered by the Django web framework. Django projects can contain many apps.
2. Django app - a small library designed to represent a single aspect of a project. An app is ideally self contained and can be reuseable in many Django projects.
3. Third party package - Django apps that have been published for download. [see here](https://djangopackages.org/).  

You can think of your house or apartment as your django project. An app would be a specific piece of furniture or appliance. A package would be a specific piece of furniture or appliance that is at the store waiting for you to pick it up, bring it home, and add it to your project.

Creating apps:

1. Run the command: $ python manage.py startapp <appNameHere>
 
 ```shell
 $ python manage.py startapp flashcards
 ```
 
 2. Add flashcards to INSTALLED_APPS in settings.py.  
 
 **settings.py**
 ```python
 INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'flashcards'
]
 ```
 
 3. Create a urls.py file in your app folder. It will be similar to the ROOT_URLCONF (by default the urls.py in the project package, the same directory as settings.py) but does not need any references to the admin panel. Here is an example:
 
 **flashcards/urls.py**
 ```python
 from django.conf.urls import url

from . import views

urlpatterns = [
    url(r'^$', views.home, name='home'),
]
 ```
 
 4. Now we need to create the view that this url is mapping to. This will be the views.py in the app directory NOT the views.py in the project package (the directory where settings.py is).
 
 **flashcards/views.py**
 ```python
 from django.http import HttpResponse

def home(request):
    '''
    Renders flashcard app home page
    '''
    return HttpResponse('Welcome to the flashcard app')
 ```
 
 5. Finally, we need to link to ROOT_URLCONF to the new flashcards urls.py file. Change the urlpatterns variable in the ROOT_URLCONF file to the following:
 
 **djangocc/urls.py (in project package)**
 ```python
 urlpatterns = [
    url(r'^$', views.home, name='home'),
    url(r'^flashcards/', include('flashcards.urls', namespace='flashcards')),
    url(r'^admin/', admin.site.urls),
]
```

### Creating A Model
[back to top](#django-crash-course-quick-reference)  
[watch video](https://youtu.be/YFdVuaSxZh8)  

Now that we have our flashcard configured and the ROOTURL conf linking to the flashcard apps urls.py (by using include), we can create our first model. Models allow us to define our database layout. What we define in our model ends up become our database schema. So if we have a model "Flashcard" with attributes "title" and "description", that means our database will have a table for "Flashcard" with three columns "id" (automatically defined by django), "title", and "description". 

If this concept of databases is new to you, think of an excel spreadsheet called "Flashcard" with three columns "id", "title", and "description". We can add need rows to the spreadsheet and put the values we need in the columns. We can also edit and delete the rows on the spreadsheet.

Lets create our first model, we will keep it very basic:

**flashcards/models.py**
```python
class Deck(models.Model):
	title = models.CharField(max_length=64, null=False, blank=False)
 	description = models.CharField(max_length=255, null=False, blank=True)
```

We added the model deck and gave it two attributes, title and description, which are both of the CharField model field types. See more documentation on model fields [here](https://docs.djangoproject.com/en/1.11/ref/models/fields/)



Because we made changes to how we want our database configured, we need to tell django to update. We use two commands for this:
1. python manage.py makemigrations
2. python manage.py migrate

After these commands have been run, we can open the shell and create our first database entries!

```shell
python manage.py shell
```

This will open the interpreter.

```python
>>> # import the model, so we can use it
>>> from flashcards.models import Deck
>>> # create a new deck
>>> myDeck = Deck(title='My First Deck', description='I created this from the shell, and it's actually stored in the database')
>>> # call the save method on the myDeck object. This will "push" it to the database
>>> myDeck.save()
>>> # check to see that it is saved
>>> Deck.objects.all()
```

### Making Database Queries
[back to top](#django-crash-course-quick-reference)  
[watch video](https://youtu.be/aWDXbLZ4iOY)

Django gives an nice API that lets us create, retrieve, update, and delete (CRUD) objects. We can using this in the manage.py shell as well as in the views. Let's go through the process in the manage.py shell.

```shell
$ python manage.py shell
```

```python
>>> from flashcards.models import Deck
>>> d = deck(title='some title', description='some description')
>>> # to save the the new deck object to the database, use the save method
>>> # this creates an INSERT sql statement
>>> d.save()
>>> # You can also use the create method on the class itself which creates the object
>>> # and inserts it at the same time
>>> Deck.objects.create(title='some_title', description-'some description')
>>> 
>>> # Now lets change the title of the "d" object
>>> d.title = 'a new title'
>>> # Calling the save method now performs an UPDATE sql statement and the database is updated with
>>> # the new title for that database entry
>>> d.save()
>>> # Now lets delete the d object.
>>> d.delete()
```

Obviously we want to be able to do more than just create, read, update, and delete objects in the database. For example, we may would want to list all objects in a table, search (filter) the objects by a given keyword, sort them alphabetically, etc. To do this we use [Managers](https://docs.djangoproject.com/en/1.11/topics/db/managers/). A manager is the interface through which database query operations are provided to Django models.

When you first create a model, django gives it a default manager named "objects". The managers communicate with the database and return the results of a given query, called a QuerySet. For advanced case you can rename the manager, create custom managers, modify the initial manager, etc. But we will stick with the basics.  Now that you know how to add objects to the database, add a bunch of decks. Then try the following queries: 

1. [Deck.objects.all()](https://docs.djangoproject.com/en/1.11/ref/models/querysets/#all)
2. [Deck.objects.last()](https://docs.djangoproject.com/en/1.11/ref/models/querysets/#last)
3. [Deck.objects.first()](https://docs.djangoproject.com/en/1.11/ref/models/querysets/#first)
4. [Deck.objects.get(id=2)](https://docs.djangoproject.com/en/1.11/ref/models/querysets/#get)
5. [Deck.objects.get(title='some title')](https://docs.djangoproject.com/en/1.11/ref/models/querysets/#get)
6. [Deck.objects.count()](https://docs.djangoproject.com/en/1.11/ref/models/querysets/#count)
7. [Deck.objects.order_by('title')](https://docs.djangoproject.com/en/1.11/ref/models/querysets/#order-by)

Now try some more from the docs listed above!

### Using QuerySets In Templates
[back to top](#django-crash-course-quick-reference)  
[watch video](https://youtu.be/hyYV3IN6ejU)

Doing all these queries in the shell is great and all, but we need to be able to use them views so that our users can actually take advantage of our awesome Django skills. The good thing is, this is super easy to do. All we need to do is to pass the queryset to the template context using the view and then use template tags to iterate over it. 

1. First we need to create a directory structure for our templates in our app. Make the following directories:
  * flashcards/templates
  * flashcards/templates/flashcards
  
> Yes that last bullet is correct. We want a templates directory inside the flashcards app, and a flashcards directory inside the flashcards/templates directory. This is due to the way Django searches for the correct template to render. Make like the URLs, it searches through a list and returns the FIRST one with the name it is looking for. In this case it will be 'home.html'. The problem is that there is another 'home.html' in the templates directory in our root directory (where manage.py is) that serves as our overall home page. Yes you could just rename your flashcards template 'home.html' but that fixes the symptom, not the problem. You can still have collisions with other templates if you are not very careful with your naming. Using the nested "flashcards/templates/flashcards/" directory to store your flashcard specific templates will make things much easier to maintain.

2. Change your flashcards views.py to include a variable of type QuerySet and pass it into the template context:

**flashcards/views.py**
```python
from django.shortcuts import render
from .models import Deck

# Create your views here.
def home(request):
    '''
    Renders the FLASHCARD app home template
    '''
    qs = Deck.objects.order_by('-title')
    context = {'decks': qs}
    return render(request, 'flashcards/home.html', context)
```

3. And finally copy the djangocc/templates/home.html to flashcards/templates/home.html and change it to iterate over the queryset:

```html
{% load static %}
<!DOCTYPE html>
<html>
  <head>
    <title>uStudy</title>
    <link rel='stylesheet' href="{% static 'css/style.css' %}" />
  </head>
  <body>
      <nav>
        <a href="">uStudy</a> |
        <a href="">Decks</a> |
        <a href="">About</a> |
        <a href="">Contact</a>
      </nav>

      {% if decks %}
        <ul>
          {% for deck in decks %}
            <li>{{deck.title}}</li>
          {% endfor %}
        </ul>
      {% else %}
        <h1>No Decks Found! Contact an Admin!</h1>
      {% endif %}

  </body>
</html>
```

### Creating a Base template
[back to top](#django-crash-course-quick-reference)  
[watch video](https://youtu.be/KTjtfTZFtWo)

Most websites have a header and footer that remain the same on every page. As you navigate around the webpage, the content between the two is normally the only thing that changes. We have seen how to create templates but it gets tedious having to a write an entirely new HTML page for every new page we want to add to our application. We end up have to copy the headers and footers every single time. That is not fun.

Django has a way around this issue for us and it is called [Template Inheritance](https://docs.djangoproject.com/en/1.11/ref/templates/language/#template-inheritance). Template inheritance allows to write a single HTML page, add a few "block" tags to it, and then reuse that template multiple times changing ONLY what is between the block tags. This is called "extending" a template.

First lets create a new html in the root templates directory called base.html:

**base.html**
```html
{% load static %}
<!DOCTYPE html>
<html>
  <head>
    <title>uStudy</title>
    <link rel='stylesheet' href="{% static 'css/style.css' %}" />
  </head>
  <body>
      <nav>
        <a href="">uStudy</a> |
        <a href="">Decks</a> |
        <a href="">About</a> |
        <a href="">Contact</a>
      </nav>

      {% block content %}
      {% endblock %}

  </body>
</html>
```

We took the original home.html and replaced the contents between the navbar and the end of the page with the {% block content %}{% endblock %} tags. This creates a block that the django templating engine will recognize when it renders the template. Now we can just extend the base.html and add our custom content by declaring the block/endblock tags again. 

Our home.html becomes:

**home.html**
```html
{% extends 'base.html' %}

{% block content %}
<div class='homepage-content'>
  <div class='homepage-banner'>
    <h1>uStudy</h1>
    <hr>
    <h4>Harness the Power of U!</h4>
    <a class='button' href="">Get Started</a>
  </div>
</div>
{% endblock %}
```

And our flashcards home.html becomes:

**flashcards/home.html**
```html
{% extends 'base.html' %}

{% block content %}
{% if decks %}
  <ul>
    {% for deck in decks %}
      <li>{{deck.title}}</li>
    {% endfor %}
  </ul>
  {% else %}
    <h1>No Decks Found! Contact an Admin!</h1>
  {% endif %}
{% endblock %}
```

Now lets add the "url" template tag to the anchor tags in our base.html, this will update the navbar links for ALL pages that inherit (or "extend") from this template!

>>IMPORTANT: the url tag returns an absolute path referencing matching a given view an optional parameters. The syntax is
>> {% url 'someName' %} where 'someName' is the name keyword for the url you want to match. So to match the url with the name "home"
>> in the ROOT_URLCONF you would use {% url 'home' %}. You can also use the namespace of an application to reference the apps url.py.
>> To reference the flashcards app url with the name "home" you would use {% url 'flashcards:home' %}.

**base.html**
```html
<nav>
  <a href="{% url 'home' %}">uStudy</a> |
  <a href="{% url 'flashcards:home' %}">Decks</a> |
  <a href="">About</a> |
  <a href="">Contact</a>
</nav>
```

### Models and Many-To-One Relationships
[back to top](#django-crash-course-quick-reference)  
[watch video](https://youtu.be/uRNNv6Fy-eE)

Just having decks in our database doesn't do much for us. We already said that each deck should have a bunch of flashcards to go with it. Let's create the flashcard model, the only new thing you will see is the [ForeignKey field](https://docs.djangoproject.com/en/1.11/ref/models/fields/#foreignkey). The ForeignKey field takes two required positional arguments: the class to which the model is related (Deck in our case) and the "[on_delete](https://docs.djangoproject.com/en/1.11/ref/models/fields/#django.db.models.ForeignKey.on_delete)" option. This creates a foreign key relationship between the parent (the deck in our case) and the child (this flashcard). Whenever our Deck is deleted, all the flashcards will be deleted as well (due to us setting on_delete=models.CASCADE).

Add the following to the bottom of flashcards/models.py:
**flashcards/models.py**
```python
class Card(models.Model):
	parentDeck = models.ForeignKey(Deck, on_delete=models.CASCADE)
	front = models.TextField()
	back = models.TextField()
```

Create a few flashcards in the shell like you previously did. You can access all the flashcards in a deck by using the card_set manager. 

**python manage.py shell**
```python
>>> from flashcards import Deck, Card
>>> d1 = Deck.objects.first()
>>> d1.article_set.all()
```
### The Django Admin Panel
[back to top](#django-crash-course-quick-reference)  
[watch video](https://youtu.be/QqyEBTXSojg)

Let's say you are building a django powered web application for a client who does not know how to use the shell. Woah, deal breaker right?!? The client won't be able to add anything to the database!

Now you might say..."I remember you saying something about an admin panel that allows me to create, read, update, and delete database entries in a previous video. The one where we made our super user?"

That's right! Django comes with an awesome admin panel that we will use from here on when it comes to modifying our database. First we will configure our admin site to use our Flashcards app models and then we will customize it to our own needs.

1. Open flashcards/admin.py and "register" the model with the admin site.

**flashcards/admin.py**
```python
from django.contrib import admin
from .models import Deck, Card

admin.site.register(Deck)
admin.site.register(Card)
```

2. Log in to your admin panel. That's it!

### Admin Panel Options
[back to top](#django-crash-course-quick-reference)  
[watch video](https://youtu.be/QqyEBTXSojg)  
[watch video on options](https://youtu.be/1BVF5coZ0TQ)

The admin panel has many options that allow you to customize it to your specific needs. Let's jump in. [docs here](https://docs.djangoproject.com/en/1.11/ref/contrib/admin/#modeladmin-options).

1. Previously we just used admin.site.register(ClassNameHere) to register our models and get the default layout. Well, we won't be using the default layout anymore so we need to refactor our code here. The ModelAdmin class is a representation of a model in the admin interface. We have to create our own representation of the ModelAdmin class.

**flashcards/admin.py**
```python
from django.contrib import admin
from .models import Deck, Card

Class DeckAdmin(admin.ModelAdmin):
    pass

Class CardAdmin(admin.ModelAdmin):
    pass

# Register your models here.
admin.site.register(Deck, DeckAdmin)
admin.site.register(Card, CardAdmin)
```

2. Let's add an "active" field to our Deck model. This way we can create new decks and not "release" them to our users while we are still busy adding cards to them. When we are done adding all the cards on a new deck, we can update the Deck object to be active.

**flashcards/models.py**
```python
class Deck(models.Model):
    title = models.CharField(max_length=64, null=False, blank=False)
    description = models.CharField(max_length=255, null=False, blank=True)
    is_active = models.BooleanField(default=False)

    def __str__(self):
        return self.title
```

3. Make migrations and migrate

4. Let's display the value of the active field for the Deck in the admin panel. We will use the [list_display option](https://docs.djangoproject.com/en/1.11/ref/contrib/admin/#django.contrib.admin.ModelAdmin.list_display)

**flashcards/admin.py**
```python
Class DeckAdmin(admin.ModelAdmin):
    list_display=('title', 'active')
```

5. A value in list display can be a string representing on attribute on the model itself. That's fancy talk for saying we can write a method on our model (in models.py) and use it on our list display. Check it out.

**flashcards/models.py**
```python
class Deck(models.Model):
    title = models.CharField(max_length=64, null=False, blank=False)
    description = models.CharField(max_length=255, null=False, blank=True)
    is_active = models.BooleanField(default=False)

    def __str__(self):
        return self.title
	
    def get_number_of_cards_as_str(self):
        num = self.card_set.count()
	return '%s' %(num)
    get_number_of_cards.short_description = 'Card Count'
```

**flashcards/admin.py**
```python
Class DeckAdmin(admin.ModelAdmin):
    list_display=('title', 'is_active', 'get_number_of_cards_as_str')
```

6. Now lets add a filter, so the user can easily filter by active decks. We will use the [list_filter option](https://docs.djangoproject.com/en/1.11/ref/contrib/admin/#django.contrib.admin.ModelAdmin.list_filter)

**flashcards/admin.py**
```python
Class DeckAdmin(admin.ModelAdmin):
    list_display=('title', 'is_active', 'get_number_of_cards_as_str')
    list_filter=('is_active',)
```

7. Finally lets add a search field, so the user can search for a record if we have a lot of Card or Deck records. We will use the [search_fields option](https://docs.djangoproject.com/en/1.11/ref/contrib/admin/#django.contrib.admin.ModelAdmin.search_fields)

**flashcards/admin.py**
```python
Class DeckAdmin(admin.ModelAdmin):
    list_display=('title', 'is_active', 'get_number_of_cards_as_str')
    list_filter=('is_active',)
    search_fields = ['title', 'description']
```
### Admin Panel Actions
[back to top](#django-crash-course-quick-reference)  
[watch video](https://youtu.be/SGeC-0MjoRw)  

Actions allow us to change many objects at once. Here is what the [docs](https://docs.djangoproject.com/en/1.11/ref/contrib/admin/actions/) say:

>>The basic workflow of Django’s admin is, in a nutshell, “select an object, then change it.” This works well for a majority of use cases. However, if you need to make the same change to many objects at once, this workflow can be quite tedious.

Let's jump in. First we need to a write a function that gets called when the action is triggered from the admin. This is just a regular function that takes three arguments: the current ModelAdmin, and HttpRequest representing the current request, and a QuerySet containing the set of objects selected by the user.

**flashcards/admin.py**
```python
def push_live(modeladmin, request, queryset):
    queryset.update(is_active=True)
push_live.short_description = "Mark selected Decks as active"
```

Now we need to add to our DeckAdmin:  
**flashcards/admin.py**
```python
Class DeckAdmin(admin.ModelAdmin):
    list_display=('title', 'is_active', 'get_number_of_cards_as_str')
    list_filter=('is_active',)
    search_fields = ['title', 'description']
    actions = [push_live]
```

Now lets display a message to the user by modifying the push_live method.

**flashcards/admin.py**
```python
def push_live(modeladmin, request, queryset):
    rows_updated = queryset.update(is_active=True)
    if rows_updated == 1:
        message_bit = "1 deck was"
    else:
        message_bit = "%s decks were" % rows_updated
    modeladmin.message_user(request, "%s successfully marked as active." % message_bit)

push_live.short_description = "Mark selected Decks as active"
```

### Creating A Form
[back to top](#django-crash-course-quick-reference)  
[watch video 1](https://youtu.be/4Ry5Hb0HSas)  
[watch video 2](https://youtu.be/D4MB78chALI)

Django has a powerful way of handling forms for us. But first we will create our own HTML form to get an introduction to the form process. [docs on forms](https://www.w3schools.com/html/html_forms.asp).

>IMPORTANT: We normally use one of two types of requests when dealing with forms. GET and POST requests. GET requests add the parameters to the url, this is good for searching, redirecting, and creating shareable urls. POST requests send the data discreetly to the server, this is good for dealing with sensitive data such as usernames and passwords. [click here for more information](https://www.w3schools.com/TAgs/ref_httpmethods.asp)

First, lets create a new url-view-template in the flashcards app that we will use to create new Decks.

**flashcards/urls.py**
```python
urlpatterns = [
    url(r'^$', views.home, name='home'),
    url(r'decks/create', views.createDeck, name='createDeck')
]
```

**flashcards/views.py**
```python
def createDeck(request):
    '''
    Renders a template used to accept POST requests 
    to create a new Deck
    '''
    if request.method == 'POST':
        print('*******************')
        print(request.POST)
        print('*******************')
    context = {}
    return render(request, 'flashcards/createCard.html', context)
```

**flashcards/templates/flashcards/createDeck.html**
```html
{% extends 'base.html' %}

{% block content %}
<form method="POST">
  {% csrf_token %}
<input type="text" name="input1"/>
<button type='submit'>Submit</button>
</form>
{% endblock %}
```

>IMPORTANT: Notice the csrf_token tag? CSRF stands for cross site request forgery. It is an attack in which an attacker would create their own form and their computer and direct it to submit to our server. THIS IS BAD! the csrf_token generates a unique token which Django uses to verify the post submission origininated from our applications.

Now run your server, navigate to localhost:8000/flashcards/decks/create, type something into the text input, and submit the form. If you look at your server terminal window, you will see something similar to the following:

```python
<QueryDict: {'csrfmiddlewaretoken': ['u2zi591l5YufP6FB7cImyRj3tnfa36hOHSWMgrZxHOUhqIJnTtMHqK2mP9OoCjBI'], 'input1': ['asdasd']}>
```

That is the result of the form that we printed out from our view. You can see the unique CSRF token that was genereated (csrfmiddlewaretoken) and the value of the form input field we gave the name 'input1' to.

Now lets finish our form and actually save the information to the database. Our url is done, we only have to do some changes in the template to add the new fields and write the logic in the view to capture the post data and save it.

**flashcards/templates/flashcards/createDeck.html**
```html
{% extends 'base.html' %}

{% block content %}
<form method="POST">
  {% csrf_token %}
Title: <input type='text' name="form_title"><br>
Description: <input type='text' name="form_description"><br>
Is Active? <input type='checkbox' name='form_is_active'><br>
<input type="submit" value="Submit Form">
</form>
{% endblock %}

```

**flashcards/views.py**
```python
def createDeck(request):
    '''
    Renders the form to add new decks to the database
    '''
    if request.method == 'POST':
        title_input = request.POST.get('form_title', None)
        description_input = request.POST.get('form_description', None)
        if 'form_is_active' in request.POST:
            is_active_input = True
        else:
            is_active_input = False
        new_deck = Deck(
                        title=title_input,
                        description=description_input,
                        is_active=is_active_input)
        new_deck.save()
        print('************ NEW DECK SAVED ****************')
    context = {}
    return render(request, 'flashcards/createDeck.html', context)
```

### Model Forms
[back to top](#django-crash-course-quick-reference)  
[watch video 1](https://youtu.be/Wwjxa7XicOs)  
[watch video 2](https://youtu.be/OafjU5BtJRI)

Creating our own forms using html and processing the post in our view is always an option. However, it becomes repetitive when we have forms with fields that map closely to our models. Thankfully django provides us the ModelForm class. This is handy because it allows django to validate the form before it is saved to the database and it simplifies our HTML templates.

First let's create a new file called "forms.py" in our flashcards app to house our new Django driven ModelForm.

**flashcards/forms.py**
```python
from django.forms import ModelForm
from .models import Deck

class DeckForm(ModelForm):
   '''
   Form mapping to the Deck model
   '''
   class Meta:
       model = Deck
       fields = ['title', 'description', 'is_active']
```

Now we can refactor our view to use the new form:

**flashcards/views.py**
```python
from .forms import DeckForm

def createDeck(request):
    '''
    Renders the form to add new decks to the database
    '''
    if request.method == 'POST':
        # create the form isntance, and populate with data from the request
        form = DeckForm(request.POST)
        # check if the form is valid
        if form.is_valid():
            #save the form, this saves the object to the database
            form.save()
    else:
        form = DeckForm()
    context = {'form': form}
    return render(request, 'flashcards/createDeck.html', context)
```

Now we finally make some changes to our template to use the new "form" variable we passed into the template (using the context in the view).

**flashcards/templates/flashcards/createDeck.html**
```html
{% extends 'base.html' %}

{% block content %}
<form method="POST">
  {% csrf_token %}
  <table>
     {{ form.as_table }}
  </table>
  <input type="submit" value="Submit" />
</form>
{% endblock %}
```

Finally let's edit our view so it redirects the user back to the flashcards home page. 
In the createDeck view add the following line just below the deck.save():

**flashcards/views.py**
```python
	    return HttpResponseRedirect('/flashcards')
```

and make sure to import it at the top of the file. 

**flashcards/views.py**
```python
from django.shortcuts import (
        HttpResponseRedirect,
        render,
    )
```

### Dynamic Url Parameters and Editing ModelForms
[back to top](#django-crash-course-quick-reference)  
[watch video](https://youtu.be/wowu8vmPNI0)  

We should also create a way to edit Decks, otherwise the users can change the status of the decks from inactive to active (or vice versa). They also may want to edit the title or description later. This creates a unique challenge in that we first have to "get" the individual deck object from the database. To get the deck from the database we need some type of "lookup" field to search the database for. For this we will use the id of the deck object and we will pass it from the url to the view using a "[named group](https://docs.djangoproject.com/en/1.11/topics/http/urls/#named-groups)".

**flashcards/urls.py**
```python
urlpatterns = [
    url(r'^$', views.home, name='home'),
    url(r'decks/create/', views.createDeck, name='createDeck'),
    url(r'decks/edit/?P(<deck_id>[\d]+)', views.editDeck, name='editDeck'),
]
```

Now that "named group" can be access in the corresponding view by passing the name as an argument:

**flashcards/views.py**
```python
def editDeck(request, deck_id):
```

Now lets finish the view, it will be VERY similar to the createDeck view. The only difference will be that we will get the object from the database using [get_object_or_404](https://docs.djangoproject.com/en/1.11/topics/http/shortcuts/#get-object-or-404) and then passing it into the form using the "instance" keyword argument. We can even use the same template!


> IMPORTANT: make sure to import get_object_or_404 from django.shortcuts.

**flashcards/views.py**
```python
def editDeck(request, deck_id):
	'''
	Renders a form allowing a user to edit a card
	'''
	deck_obj = get_object_or_404(Deck, id=deck_id)
	if request.method == 'POST':
		form = DeckForm(request.POST, instance=deck_obj)
		if form.is_valid( ):
			form.save( )
			return HttpResponseRedirect('/flashcards')
	else:
		form = DeckForm(instance=deck_obj)
	context = {'form': form,}
	return render(request, 'flashcards/createDeck.html', context)
```

Finally we can add a link to edit the decks from the flashcards home page.

**flashcards/templates/flashcards/home.html**
```html
{% for deck in decks %}
    <li>{{deck.title}} - <a href="{% url 'flashcards:editDeck' deck.id %}"> edit </a></li>
{% endfor %}
```
### Using A View To Delete An Object
[back to top](#django-crash-course-quick-reference)  
[watch video](https://youtu.be/h0TK8JstlGc)

Deleting an object using a view is as simple as retrieving the object from the database and then calling the delete method on it. 

First lets create a new url to handle deleting decks:

**flashcards/urls.py**
```python
urlpatterns = [
    url(r'^$', views.home, name='home'),
    url(r'decks/create/', views.createDeck, name='createDeck'),
    url(r'decks/edit/(?P<deck_id>[\d]+)', views.editDeck, name='editDeck'),
    url(r'decks/delete/(?P<deck_id>[\d]+)', views.deleteDeck, name='deleteDeck'),
]
```

Notice we are using a named group again, this is how we will get the deck_id in the view in order to retrieve a specific deck from the database.

**flashcards/views.py**
```python
def deleteDeck(request, deck_id):
    '''
    Deletes the deck whose id == deck_id
    '''
    deck_obj = get_object_or_404(Deck, id=deck_id)
    deck_obj.delete()
    return HttpResponseRedirect('/flashcards')
```

Notice the above view does not render a template. Instead we will create a button in the template that renders the form to add/edit the deck and have the button call this view. First lets rename the createDeck.html to a more suitable name createAndEditDeck.html and add the button if we are in the "edit mode" only.

**flashcards/templates/flashcards/createAndEditDeck.html**
```html
{% extends 'base.html' %}

{% block content %}
<form method="POST">
  {% csrf_token %}
  <table>
    {{ form.as_table }}
  </table>
<input type="submit" value="Submit Form">
</form>

{% if edit_mode %}
  <p>Do you want to delete this deck?</p>
  <a href="{% url 'flashcards:deleteDeck' deck_obj.id %}"> Delete This Deck</a>
{% endif %}

{% endblock %}
```

Notice we are now referencing two new variables in the template: edit_mode and deck. Because we only want to see this button while we are editing, we can simply pass use the editDeck view to pass these variables to the template context:

**flashcards/views.py**
```python
def editDeck(request, deck_id):
    '''
    Renders the form to edit information about a deck object
    '''
    deck_obj = get_object_or_404(Deck, id=deck_id)
    if request.method == 'POST':
        # create the form isntance, and populate with data from the request
        form = DeckForm(request.POST, instance=deck_obj)
        # check if the form is valid
        if form.is_valid():
            #save the form, this saves the object to the database
            form.save()
            return HttpResponseRedirect('/flashcards')
    else:
        form = DeckForm(instance=deck_obj)
    context = {'form': form, 'edit_mode':True, 'deck_obj':deck_obj}
    return render(request, 'flashcards/createAndEditDeck.html', context)
```
### Using Named Urls In Views
[back to top](#django-crash-course-quick-reference)  
[watch video](https://youtu.be/Aj0BFPhZXWo)

We know the url template tag allows us to use the named urls ({% url 'name' %} or {% url 'namespace:name' %}) and even pass arguments to the urls. It would be nice to have the same functionality in views. Right now, everytime we redirect the user using HttpResponseRedirect we harcode a url. Hardcoding is bad because if we change our url patterns in the future we would then have to go a change every hardcoded url. This is primary reason we use the url template tag in templates.

We can achieve the same functionality of the url template tag in a view by using the [reverse function](https://docs.djangoproject.com/en/1.11/ref/urlresolvers/#reverse).

Open views.py, import reverse from django.urls, then change all hardcoded HttpResponseRedirects to use the reverse url lookups. One example is given below:

```python
from django.urls import reverse
return HttpResponseRedirect(reverse('flashcards:home'))
```

If the URL accepts arguments, you may pass them in args. For example:

```python
from django.urls import reverse
return HttpResponseRedirect(reverse('flashcards:viewDeck', args=[10]))
```

### Introduction To Automated Testing
[back to top](#django-crash-course-quick-reference)  
[watch video 1](https://youtu.be/UvQLp6F42ec)  
[watch video 2](https://youtu.be/l4ZdslbnFjQ)  
[watch video 3](https://youtu.be/X1PnAz7gpMI)  
[watch video 4](https://youtu.be/JdgnWQH5nVo)  

Testing is a big topic. Testing a web application is a huge topic. There are many layers of an web app that could be tested: HTTP-level request handling, form validation and processing, template rendering, model logic, etc. There is even a software development process where programmers write tests for their code before they even write their code called [test-driven development](https://en.wikipedia.org/wiki/Test-driven_development). Ultimately, testing is vital to production level development and it is something you should have some exposure to. 

While the testing could be an entire course in itself, we will focus on just a basic introduction. We will use test-driven development to write tests that will verify our flashcard navigation functionality is working correctly.

1. First open flashcards/tests.py. This is where we will put our tests. We will define a class called CardTestCase that subclasses django's built in TestCase class. Then we will define some variables and set them to None. 

**flashcards/tests.py**
```python
from django.test import TestCase
from .models import Card

class CardTestCase(TestCase):
    deck = None
    card1 = None
    card2 = None
    card3 = None
```

2. Now we want to set up our testing fixture. This will create a new empty testing database and thus we need to create new deck and card objects in the testing database. We do this using the setUp() method.

**flashcards/tests.py**
```python
def setUp(self):
        '''
        Sets up our testing fixture and creates objects
        which we can use in following tests
        '''
        self.deck = Deck.objects.create(title='test_deck_1')
        self.card1 = Card.objects.create(
                                            parentDeck = self.deck,
                                            front = 'front of card1',
                                            back = 'back of card1'
                                        )
        self.card2 = Card.objects.create(
                                            parentDeck = self.deck,
                                            front = 'front of card2',
                                            back = 'back of card2'
                                        )
        self.card3 = Card.objects.create(
                                            parentDeck = self.deck,
                                            front = 'front of card3',
                                            back = 'back of card3'
                                        )
```

3. Now lets create our first test case. Our test cases will be methods with names starting with "test_", for example: "test_some_custom_test".

**flashcards/tests.py**
```python
def test_starting_conditions(self):
        '''
        Check if deck and cards exists
        '''
        self.assertIsInstance(self.deck, Deck)
        self.assertIsInstance(self.card1, Card)
        self.assertIsInstance(self.card2, Card)
        self.assertIsInstance(self.card3, Card)
```

4. So far our tests.py looks like: [source here](https://github.com/highfivecode/DjangoCrashCourse/blob/af2f3117a5c7d4e492a1096481bcb5fc8533b28d/flashcards/tests.py). Finally, we can run all these tests using manage.py

```shell
$ python manage.py test
```
      
#### PART 2

Now lets write our first test that we know is going to fail.

**flashcards/tests.py**
```python
def test_card_has_prev(self):
        '''
        The first card does not have a prev card.
        All other cards do.
        '''
        self.assertFalse(self.card1.has_prev_card())
        self.assertTrue(self.card2.has_prev_card())
        self.assertTrue(self.card3.has_prev_card())
```

If we run our test, it fails. Well of course it fails, we haven't even written the has_prev_card() method in the Card model yet! So lets do that.

**flashcards/models.py**
```python
class Card(models.Model):
	<snipped for brevity>
	
    def has_prev_card(self):
        '''
        Returns true if the card is not the first card
        in the deck.
        '''
        first_card_in_deck = self.parentDeck.card_set.first()
        if self == first_card_in_deck:
            return False
        return True
```

Now if we run our test. We see it passed! Let's finish this part by writting the test and then the code to see if a card has a next card:

**flashcards/tests.py**
```python
    def test_card_has_next(self):
        '''
        The last card does not have a next card.
        All other cards do.
        '''
        self.assertTrue(self.card1.has_next_card())
        self.assertTrue(self.card2.has_next_card())
        self.assertFalse(self.card3.has_next_card())
```

**flashcards/models.py**
```python
class Card(models.Model):
	<snipped for brevity>
	
    def has_next_card(self):
        '''
        Returns true if the card is not the last card
        in the deck
        '''
        last_card_in_deck = self.parentDeck.card_set.last()
        if self == last_card_in_deck:
            return False
        return True
```

#### Part 3 And Part 4

Part 3 and 4 did not introduce new topics, they just simply included writing more test cases and the corresponding code in the model. See the final versions:  
[tests.py](https://github.com/highfivecode/DjangoCrashCourse/blob/5ecd9fd68aa48d50b68e44c7d31fbc21abef394f/flashcards/tests.py)  
[models.py](https://github.com/highfivecode/DjangoCrashCourse/blob/5ecd9fd68aa48d50b68e44c7d31fbc21abef394f/flashcards/models.py)  
