# DjangoTutorial

This follows the tutorial on [DjangoProjects.org](https://docs.djangoproject.com/en/3.0/intro/tutorial01/) to build a polling app.

1. Setup a virtual environment with `python -m venv .venv`
2. Direct your editor to this environment.
    - *In VS Code* create a folder called `.vscode `.
    - *In VS Code* add a file `settings.json` with `{"python.pythonPath": "${workspaceFolder}\\.venv\\Scripts\\python.exe", "python.venvPath": "${workspaceFolder}\\.venv"}`
3. Make sure you have a .gitignore set up to ignore everything above.
4. Setup the required packages with `pip install -r requirements.txt`

 If you are saving into your own git to follow along, delete the folder `DjangoTutorialCode` as you will be making this. ALso if you are 

## Part 1
- To initialize a project you must run `django-admin startproject 'name'`. This will create a folder titled *name* that contains everything to start a server, here we will call it *mysite*.
- To start a server run `python manage.py runserver` will create a server at [](http:127.0.0.1:8000/).
- To create a new app run `python manage.py startapp 'name'`. This will create a base app with the name *name*. This demo will call the app *polls*

You can now create new views (or webpages) in `polls/views.py`. To give this an actual url, you will need to create a url configuration with a new file `polls/urls.py`. Here you can name this url so it can be accessed globally. To actually add it to the server, it must be included in `mysite/urls.py`.

Once you can run `python manage.py runserver` and successfuly open the page at [](http:127.0.0.1:8000/polls/) (which is where a normal *index* page leads to) then you can save your code and push to the remote.