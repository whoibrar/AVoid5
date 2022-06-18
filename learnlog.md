## Django 101

- Django is BackEnd ServerSide OpenSource framework built on Python
- Emphasis on DRY and CRUD and is somewhat opinionated (right way to do things)
- Used by Instagram Mozilla Pinterest, initally created in 2003-05 to for newspaper site

- MVC (Model View Controller) MVT (Model View Template)
- Process Flow
    - Recieve Request --> urlmatching --> view 
    - choose view --> models --r/w-(DB)--> models --> view --> template
    - dynamically populate --> webpage

### Essentials

- URLs `urls.py`
    - Redirect HTTP requests to appropriate view using URL Mapper
    - Can be used for pattern matching
- Views `views.py`
    - Request handler that processes users request
    - Access data needed to satisfy via Models
    - Uses Templates formatting to return HTML
    - ?? Function based vs Class based 
- Models `models.py`
    - Objects define structure of application
    - Provide CRUD mechanism
    - class based reperentation of database tables 
    - data is delivered as ORM (object relation mapping)
        - attributes in class reperent columns in DB
        - helps use SQL type commands without knowing SQL
        - basically models talk to DB and does all ~~dirty work~~ wizadry for us
        - Relationship Creation(1:1 and 1:M)
- Templates `<app>/templates/`
    - Structure and Layout using HTML 
    - Using placeholders to dynamically populate
    - Can be used for any file type beyond just HTML
- Apps `<root>/<app>`
    - Breaking up whole functionality of wesbite into small similar clusters
    -  Contains Templates URLs Models Views
    - Connected to main application in settings 
- More Features
    - Forms
    - CRUD ORM (also DB Managing)
    - Authentication (Registration Login Logout Reset)
    - Signals (Event Listeners)
    - Caching (render on time?)
    - Data Serializing (see later)

### How It works

- Sending Requests 
    - URL Mapper in `urls.py` maps urls with view functions
    - When matched associated view function is called and request passed
- Handling Requests
    - Reciving HTTP request to returning HTTP Response
    - 

### Commands & HelloWorld Response

```python

# check version Django
django-admin --version 

# create project named playground
django-admin startproject playground

# directory structure
playground/
├── playground/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── manage.py
└── db.sqlite3

# run server
python manage.py runserver

# go to sever
    # localhost:8000
    # http://127.0.0.1:8000/

# Create HelloWorld Response 

    ## create helloworld response in view
    ## playgrounds/views.py (create file)
        from django.shortcuts import render
        from django.http import HttpResponse

        def HelloWorld(request):
            return HttpResponse("HelloWorld")

    ## connect this to url response
    ## playground/urls.py 
        from django.contrib import admin
        from django.urls import path,include
        from . import views 

        urlpatterns = [
            path("", views.HelloWorld, name="HelloWorld"),
            path('admin/', admin.site.urls),
        ]

    ## access localhost:8000
        ## helloworld
    
    ## What Just Happened 
        ## request is send to urls.py file
        ## that looks passes the helloword func defined in views
        ## thsi function returns the string "HelloWorld"

# create app named wan
python manage.py startapp wan

# directory structure
playground
├── db.sqlite3
├── manage.py
├── playground
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
└── wan
    ├── __init__.py
    ├── admin.py
    ├── apps.py
    ├── migrations
    │   └── __init__.py
    ├── models.py
    ├── tests.py
    └── views.py


# HelloWorld using apps 

    ## undo all changes done previously
    ## or start fresh 

    ## playground/wan/models.py file
        from django.http import HttpResponse

        def HelloWorld(request):
            return HttpResponse("HelloWorld")

    ## playground/wan/urls.py created file
        from django.urls import path
        from . import views

        urlpatterns = [
            path('', views.index, name='index'),
        ]

    ## connecting playgrounds/wan/urls.py to playgrounds/urls.py
        from django.urls import include, path
        urlpatterns = [
            path('members/', include('members.urls')),
            path('admin/', admin.site.urls),
        ]

    ## accessing 
        ## localhost:8000/wan 
        ## you get hello world as reponse

    ## What Just Happened
        ## access localhost:8000/wan
        ## here request is initially made to `playground/urls.py`
        ## which then matches and passes to `playgroud/wan/urls.py`
        ## function is invoked that returns string "HelloWorld" as response

    ## How Different from previous
        ## Here we are seperating the functionality into components
        ## each part can be segmented and constrained 

```


## Django Links

- Official 
    - [Django Website](https://www.djangoproject.com/)
    - [Django documentation contents](https://docs.djangoproject.com/en/4.0/contents/)
    - 

- Guides
    - [Django introduction - MDN](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Introduction)
    - [Django by Example - YouTube](https://www.youtube.com/playlist?list=PLAF3anQEEkzS-mjdX7s-D63bjLWRdhuFM)


- Build With Me
    - [Build a Social Media App with Django – YouTube](https://www.youtube.com/watch?v=xSUm6iMtREA&t=291s)
    - [Django REST Framework Oversimplified - YouTube](https://www.youtube.com/watch?v=cJveiktaOSQ)



## Django Playlist

### 01-03 Django 

```
// Check Django Version
python -m django --version

// virtual environtment

    // creating virtual env
    py -m venv env
    // activating virtual env
    .\env\Scripts\activate


// run django server
python manage.py runserver

// apps in django
django single project can contain multiple apps in it

```

### 04 Admin

```
// changing the schema of post / users
>>> python manage.py makemigrations
>>> python manage.py migrate

// admin user
>>> python manage.py createsuperuser 
>>> whoibrar -> whoibrar@protonmail.com -> whoibrar 

// admin panel gui
// localhost:port /admin
```

### 05 Database

```
// for any changes to db design
// remake migrations 

// ORM -> object relational mapper 

// what we are using here
SQL lite for developement 
Postgress for production

// to view sql command
python manage.py sqlmigrate blog 0001 


// open shell command
python manage.py shell

// query users
//////////////

    >>> from django.contrib.auth.models import User
    >>> User.objects.all()
    >>> User.objects.first()
    >>> User.objects.last()

    // add filters 
    Users.objects.filter(username='whoibrar') 
        // above returns a query set, extract a user from it 
        // first() or last()

    // assigning it
    a = User.object.filter(username='john') 

    // view attributes
    a.id 
    a.pk 

    // get by id 
    b = User.objects.get(id=1)

// post 
///////

    // create posts
    post_1 = Post(title='HelloWorld',content='First post content!', author=user1)

    // save post
    post_1.save()

    // see all posts
    Post.objects.all()

// importing models
from blog.models import Post
from django.contrib.auth.models import User

// accesing fields from posts
post = Post.objects.first() // grabs the first post
post.content // display the content of the post

// !!! fix data_posted -> date_posted
// done via migration 

// Query all Posts from a user
.modelName_Set

// to get all posts by a user (whoibrar)
///////////////////////////////

    // get the user first
    >>> user = User.objects.filter(username='whoibrar').first()
    
    // get post_set
    >>> user.post_set
    
    // get all posts
    >>> user.post_set.all() // returns a queryset
    
    // post_set can be used to create posts as well
    >>> user.post_set.create(title='UnosDosTres', content='Third post in series',author=user) 
        // can skip the author field and also don't need to save

// Adding Posts to Admin Panel (GUI)
////////////////////////////////////

    // from .models import Post
    // amdin.site.register(Post)

```

### 06 user Registration

```
// making a new app
python manage.py startapp users
// add it to installed apps in settings.py

// using this new app (users) 
// ...for managing all registration stuff


// implementing the following
// form creation 
// styling
// validation 

// adding crispy forms
```

### 07 Authentication System 

```
// adding login routes 

// restring certain pages 
```

### 08 Profile Pictures

```
// extending the models to 
// ... profile pictures

// get the pillow extention
// create a model in models.py
// import to admin 
// register in admin

// user -> say particular user object
// user.profile.image -> image name
// user.profile.image.url -> location
// user.profile.imaeg.width -> dimensions

// same name conflict is avoided using hashing
```

### 09 More Profile 

```
// let updation of profile info

// image size reduction
```

### 10 CRUD 

```
// class based views 
// generic views 
    // list  
    // detailed 

// <app>/<model>_<viewtype>.html

// create posts
// update posts
// delete posts

// add another superuser


!!! CANT CREATE NEW USERS !!!
```

### 11 Paginator 


```python 

# add posts from json
import json 
from bolg.models import Post
with open('posts.json') as f:
    posts_json=json.load(f)

for post in posts_json:
    post=Post(title=post['title'], content=post['content'],author_id=post['user_id'])
    post.save()

###############
## paginator ## 
###############

>>> from django.core.paginator import Paginator
>>> posts=['1','2','3','4','5']
>>> p=Paginator(posts,2)
>>> p.num_pages #3
>>> p1 = p.page(1)
>>> p1.has_previous() #false
>>> p1.has_next() #true
>>> p1.next_page_number()


// list all posts 
// display only by a user

```


