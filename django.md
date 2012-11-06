#Introduction to Django

###Once you have Django installed, in terminal enter:

    django-admin.py startproject mysite

This will create a my site directory in your current directory. In the my site directory, the following has been created:

    mysite/
    manage.py
        mysite/
        __init__.py
        settings.py
        urls.py
        wsgi.py

To run your Django server, enter the following in your my site folder:

    python manage.py runserver 

Note, by default it is hosted at http://127.0.0.1:8000/

Take a look at the "Welcome to Django" page :)

To change the port, you can pass it when you call the run run server command:

    python manage.py runserver 8080

So that is pretty sweet, you just ran your first Django server! :)

###Setting up the database

Open up mysite/settings.py. Find the DATABASE object, and we will use sqlite3 in this example.

Lets make the following changes:

```python
ENGINE = 'django.db.backends.sqlite3'
NAME = 'absolute_path' 
```

Now that we have the database setting complete, lets sync the database:

    python manage.py syncdb

Now, lets create an app. A project can have many apps.

    python manage.py startapp polls

The following directory will be created:

    polls/
        __init__.py
        models.py
        tests.py
        views.py

Lets give our app some models, open up the models.py file and add the following:

```python
from django.db import models

class Poll(models.Model): 
    question = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')

class Choice(models.Model):
    poll = models.ForeignKey(Poll) 
    choice = models.CharField(max_length=200)
    votes = models.IntegerField()
```

Cool, so you have created two models, now to link them. In settings.py, let's add 'polls' to INSTALLED_APPS

Awesome. So now lets tell Django to include our app. 

    python manage.py sql polls

Now you will see the two create tables commands. That is super awesome. You never need to create a database manually again =)

To create those new model tables in your database, run:

    python manage.py syncdb    

Lets play with the python shell:

    python manage.py shell

….

So you noticed that Poll.objects.all() gives you: <<Poll: Poll object\> that is not helpful. >To fix this issue, we can add something to our models.py class. 

```python
    def __unicode__(self):
        return self.title
```

So now we have done too much backend stuff. Let us look at the admin features. Open up settings.py, and in INSTALLED_APPS, lets uncomment 'django.contrib.admin' and syncdb



