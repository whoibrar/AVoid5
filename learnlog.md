## Django 101

- MVC (Model View Controller) sometimes Routing MVR
- Request --> `urls.py` [`urlpatterns`] --> choose view 
- ... --> models --r/w--> DB --> templates--> webpage
- 


## More Django 

- Links
    - [Django by Example - YouTube](https://www.youtube.com/playlist?list=PLAF3anQEEkzS-mjdX7s-D63bjLWRdhuFM)
    - [Build a Social Media App with Django – Python Web Framework Tutorial - YouTube](https://www.youtube.com/watch?v=xSUm6iMtREA&t=291s)
    - [Django REST Framework Oversimplified - YouTube](https://www.youtube.com/watch?v=cJveiktaOSQ)
    - 

- Apps 
    - Breaking up whole functionality of wesbite into small similar clusters
    -  Contains Templates URLs Models Views
    - Connected to main application in settings 
- Views 
    - Processing users request when processing url
    - logic in backend and html return
    - Function based vs Class based 
- Models 
    - class based reperentation of database tables 
    - attributes in class reperent columns in DB.
    - Relationship Creation(1:1 and 1:M)
- CRUD ORM 
    - save() and delete()
    - ModelForms, Class based views
    - Also DB Managing
- Authentication
    - Registration Login Logout Reset
- Commands
- Signals 
    - Event Listeners 


## Django Playlist

### 01-03 Django 

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


### 04 Admin

// changing the schema of post / users
>>> python manage.py makemigrations
>>> python manage.py migrate

// admin user
>>> python manage.py createsuperuser 
>>> whoibrar -> whoibrar@protonmail.com -> whoibrar 

// admin panel gui
// localhost:port /admin

### 05 Database

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


### 06 user Registration

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

### 07 Authentication System 

// adding login routes 

// restring certain pages 

### 08 Profile Pictures

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

### 09 More Profile 

// let updation of profile info

// image size reduction

### 10 CRUD 

// class based views 
// generic views 
    // list  
    // detailed 

// <app>/<model>_<viewtype>.html

// create posts
// update posts
// delete posts

// add another superuser
