# DjangoTutorial

This follows the tutorial on [DjangoProjects.com](https://docs.djangoproject.com/en/3.0/intro/tutorial01/) to build a polling app.

## Setup your environment
1. Setup a virtual environment with `python -m venv .venv`
2. Direct your editor to this environment.
    - *In VS Code* create a folder called `.vscode `.
    - *In VS Code* add a file `settings.json` with
```json
{
    "python.pythonPath": "${workspaceFolder}\\.venv\\Scripts\\python.exe",
    "python.venvPath": "${workspaceFolder}\\.venv"
}
```
3. Make sure you have a .gitignore set up to ignore everything above. Also add the following to avoid getting many junk files in the repository.
```
.venv
.vscode
__pycache__
*.pyc
```
4. Setup the required packages with `pip install -r requirements.txt`

 If you are saving into your own git to follow along, delete the folder `DjangoTutorialCode` as you will be making this. ALso if you are 

## Part 1 - Initializing a Project, Server and App
- To initialize a project you must run `django-admin startproject 'name'`. This will create a folder titled *name* that contains everything to start a server, here we will call it *mysite*.
- To start a server run `python manage.py runserver` will create a server at [](http:127.0.0.1:8000/).
- To create a new app run `python manage.py startapp 'name'`. This will create a base app with the name *name*. This demo will call the app *polls*

You can now create new views (or webpages) in `polls/views.py`. You should create an index page for your app to give the app a home domain. To give this an actual url, you will need to create a url configuration with a new file `polls/urls.py`. Here you can name this url so it can be accessed globally. To actually add it to the server, it must be included in `mysite/urls.py`.

Once you can run `python manage.py runserver` and successfuly open the page at [](http:127.0.0.1:8000/polls/) (which is where a normal *index* page leads to) then you can save your code and push to the remote.

## Part 2 - Databases, models and Admin access
### Databases
Some sub-apps require database management (Admin access, authentication, etc.) and hence it is important to manage.
- To initialize a database (the default here is SQLite although PostgreSQL can be used for bigger problems) run `python manage.py migrate`
- To bring any new models from *polls* into a database run `python manage.py makemigrations polls`, this will create a new migration file with an index, since this our first we have `polls/migrations/0001_initial.py`.
- Then to see these new models as SQL `python manage.py sqlmigrate polls 0001`.
- Lastly, we run `python manage.py migrate` to add these models to the database.
Here we have just modified a database live and hence have lost nothing and won't lose anything in future modifications.

### API access 
To run and text functionality of the models that are now in the database, we can access the API with `python manage.py shell`. Anything created here does persist, so `object.delete()` is needed to get rid of anything we don't want lingering.

### Admin creation
To access the admin side of the app you will need to create a superuser and log its credentials with `python manage.py createsuperuser`. Once that exists, you can log into the internal workings of the app through [](http://127.0.0.1:8000/admin/).

Once you have explored the features and have added your models to the admin site, then you are ready to push up your changes.

## Part 3 - User-Facing Views
To incorporate python and html, we will write html files that take in javascript-like code but is interpreted as python. Inside html we can have python based functions and object recognition. Using proper templating and url name spacing is key to making sure the output looks nice and the code is unambiguous .

## Part 4 - Form processing
Here we structure the voting form better and actually get interactive controls. This all happens on the html side using embedded python. 

We also streamline the view code - promote the former functions to classes that enherit generic properties.

## Part 5 - Automated testing
Test Test Test! We can use the built in testing infrastructure in `polls/tests.py`. Here adding a class to each view/model you want to test compartmentalizes the testing. Each test must begin with *test* and the more the merrier.

You can simulate a testing environment in console using `python manage.py shell` to open the API and run the following
```python
from django.test.utils import setup_test_environment
setup_test_environment()
from django.test import Client
client = Client()
from django.urls import reverse
response = client.get(reverse('polls:index'))
response.status_code
```

## Part 6 - CSS and style sheets
There is not much content here, to have static files be served by Django, there needs to be a *STATIC_ROOT* defined. This is just a global location that Django will keep updated with `python manage.py collectstatic`.

To load a *CSS* file into an html file via Django, we will use
```html
{% load static %}

<link rel="stylesheet" type="text/css" href="{% static 'polls/style.css' %}">}
```
Be careful with the namespace of stylesheets just like with the html templates.

## Part 7 - Editing Admin display
The default admin access won't cut it for all apps and so here we edit the display, how to interact with models and relate them, and how to customize the html file.

This concludes this follow-along. I will now reuse this code to a separate financial calculator I am adding to [my website](https://mathnstein.github.io/).