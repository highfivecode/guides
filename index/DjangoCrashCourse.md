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
[QuerySets](https://docs.djangoproject.com/en/1.11/ref/models/querysets/)  
[QuerySet API](https://docs.djangoproject.com/en/1.11/ref/models/querysets)  
[Templates](https://docs.djangoproject.com/en/1.11/topics/templates/)  
[Template Language](https://docs.djangoproject.com/en/1.11/topics/templates/#the-django-template-language)
  * [Templating Tags Reference](https://docs.djangoproject.com/en/1.11/ref/templates/builtins/#ref-templates-builtins-tags)
  * [Templating Filter Reference](https://docs.djangoproject.com/en/1.11/ref/templates/builtins/#ref-templates-builtins-filters)
 
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
    days_of_week = ['monday', 'tuesday', 'wednesday', 'thursday', 'friday', 'saturday', 'sunday'
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

First lets create a new html in the root templates directory called base.py:

**base.py**
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
