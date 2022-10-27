# Fundamental
1. Check installated version ` python -m django --version`
2. Create project (mysite)
    * `django-admin startproject mysite`
3. Let’s look at what startproject created:
    ```
    mysite/
    manage.py
    mysite/
        __init__.py
        settings.py
        urls.py
        asgi.py
        wsgi.py
    ```
    * **manage.py:** A command-line utility that lets you interact with this Django project in various ways. You can read all the details about manage.py in django-admin and manage.py.
    * The inner **mysite/** directory is the actual Python package for your project. Its name is the Python package name you’ll need to use to import anything inside it (e.g. **mysite.urls**).
    * **mysite/__init__.py:** An empty file that tells Python that this directory should be considered a Python package. If you’re a Python beginner, read more about packages in the official Python docs.
    * **mysite/settings.py:** Settings/configuration for this Django project. Django settings will tell you all about how settings work.
    * **mysite/urls.py:** The URL declarations for this Django project; a “table of contents” of your Django-powered site. You can read more about URLs in
    * **mysite/asgi.py**: An entry-point for ASGI-compatible web servers to serve your project. See How to deploy with ASGI for more details.
    * **mysite/wsgi.py:** An entry-point for WSGI-compatible web servers to serve your project. See How to deploy with WSGI for more details.

# The development server¶

Let’s verify your Django project works. Change into the outer mysite directory, if you haven’t already, and run the following commands:

* ` python manage.py runserver`
* `python manage.py runserver 8080`
* `python manage.py runserver 0.0.0.0:8000`
    * I just added the ip in ALLOWED_HOSTS property in the file **<your_app_path>/settings.py.** <br>`ALLOWED_HOSTS = ["0.0.0.0"]`

### Note:Automatic reloading of runserver
>The development server automatically reloads Python code for each request as needed. You don’t need to restart the server for code changes to take effect. However, some actions like adding files don’t trigger a restart, so you’ll have to restart the server in these cases.

# Creating the Polls app
*  focus on writing code rather than creating directories.

# Projects vs. apps
> What’s the difference between a project and an app? An app is a web application that does something – e.g., a blog system, a database of public records or a small poll app. A project is a collection of configuration and apps for a particular website. A project can contain multiple apps. An app can be in multiple projects.

*  we’ll create our poll app in the same directory as your manage.py file so that it can be imported as its own top-level module, rather than a submodule of mysite
* To create your app, make sure you’re in the same directory as **manage.py** and type this command:
```
python manage.py startapp polls
```
### That’ll create a directory polls, which is laid out like this:
``` 
polls/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py
```
This directory structure will house the poll application.

# Write your first view
* Let’s write the first view. Open the file **polls/views.py** and put the following Python code in it:

```
from django.http import HttpResponse


def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")
```

* his is the simplest view possible in Django. To call the view, we need to map it to a URL - and for this we need a URLconf.

* To create a URLconf in the polls directory, create a file called **urls.py.** Your app directory should now look like:
```
from django.urls import path

from . import views

urlpatterns = [
    path('', views.index, name='index'),
]
```
The next step is to point the root URLconf at the **polls.urls** module. In **mysite/urls.py**, add an import for **django.urls.include** and insert an **include()** in the **urlpatterns list,** so you have:

```
The include() function allows referencing other URLconfs. Whenever Django encounters include(), it chops off whatever part of the URL matched up to that point and sends the remaining string to the included URLconf for further processing.

The idea behind include() is to make it easy to plug-and-play URLs. Since polls are in their own URLconf (polls/urls.py), they can be placed under “/polls/”, or under “/fun_polls/”, or under “/content/polls/”, or any other path root, and the app will still work.

When to use include()

You should always use include() when you include other URL patterns. admin.site.urls is the only exception to this.
```

## Go to http://localhost:8000/polls/ in your browser, and you should see the text “Hello, world. You’re at the polls index.”, which you defined in the index view.

The path() function is passed four arguments, two required: route and view, and two optional: kwargs, and name. At this point, it’s worth reviewing what these arguments are for.





