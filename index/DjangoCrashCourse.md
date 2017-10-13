[Back to Guides](../README.md)
# Django Crash Course Quick Reference

##### Django Documentation References
[Django Homepage](https://docs.djangoproject.com)  
[Django Packages](https://djangopackages.org/)     
[Making Queries](https://docs.djangoproject.com/en/1.11/topics/db/queries/)  
[Managers (Querysets)](https://docs.djangoproject.com/en/1.11/topics/db/managers/)  
[Migrations](https://docs.djangoproject.com/en/1.11/topics/migrations/)  
[Model Fields](https://docs.djangoproject.com/en/1.11/ref/models/fields/)  
[QuerySets](https://docs.djangoproject.com/en/1.11/ref/models/querysets/)  
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
