Today [12/18/2021] is Framework Friday. 

On each Friday, I will [research] and attempt to [learn] and [review] a new framework. Most of the frameworks will be 
web related as I am a Web Developer by profession. Other frameworks will appeal to Software Engineers as well as Web Developers. 
This Friday, we research and review a voted top pick. Many of you were suggesting Django. While Django is the web framework 
for perfectionists with deadlines, we decided to keep the backend devs in mind this round and present for Django REST Framework! 

Let's begin.

[RESEARCH]

The Django REST framework is a powerful and flexible toolkit for building customizable Web APIs.

This week's [RLR] will focus on the Authentication policy, specifically the packages one can use.
I don't know about you, but I struggle with API authentication, s
o this will indeed be a learning while sharing experience in real-time.

The research will overview the framework from a first glance. Think of the 5 "W"s.
To learn will cover the How. An in-depth look for junior devs. A refresher for senior devs.
The review will reveal some obvious and not so obvious aspects of the framework.


For starters, to see that the requirements include Python (3.8) and Django (3.2) series is a relief. 
Many of the OSes I use come with at least Python 3.6. Django, of course should only be installed in environments 
that actually use it, so only officially recommended uses apply. see [virtualenv, pyenv]


Another great aspect of the Django REST framework is the support. Although the suggested IRC channel [#restframework] 
has roughly 9 users in attendance, the [REST] framework discussion group seems the primary way to get support. 
It is still early in the research, so we will only later find out if support is needed during our learning stage.


Perhaps the most impressive (and this is my subjective opinion) is the [django-rest-framework.org] website.
It provides extensive documentation and even hosts tutorials (which we will be using for learning) to get users started.
Granted it isn't the most elegant looking site, but it works flawlessly and is obviously designed with developers in mind. 
If users aren't willing to read the docs, then users can join the Stack Overflow conversations to get up to speed. 


[LEARN]

After setting up a virtual environment, it is time to install Django REST framework. [djangorestframework]

I started to use an environment already in-progress but decided to give readers a from-scratch scenario. 
Often, it is much easier to follow set-up with no pre-configured packages.

However, I do recommend that if you are setting up from in-progress application to start off early. 
You can use the getting started with Django tutorial or follow one on the REST framework site.

For this installation and usage, we will be using python3.8 and django3.2. 
If you wish you can do python3.10 and django-3.2. [https://buildmedia.readthedocs.org/media/pdf/django/3.2.x/django.pdf] 

NOTE: django-4.0 is supported in the latest REST framework release!
[django-rest-framhttps://www.django-rest-framework.org/#installationework.org/#installation]

    [commands]
    -`python3.8 -m virtualenv env`
    -`source env/bin/activate`
    -`pip install Django==3.2`
    -`pip install djangorestframwork`




If you intend to support a browsable API or wish to add filtering support, you can install optional packages.
    -markdown
    -django-filter


In naming our project, we honor the blog community. 
You may want your first time with Django and the REST framework to be more special. 
Choose whatever project and application names you prefer.


- `django-admin startproject insecure_blog`



This created the settings.py file we will use to add `rest_framework` to the `INSTALLED_APPS` setting.
Let's do that, since we are here for the framework and not just django. 

Here's what I have so far inside [/insecure_blog/insecure_blog/settings.py].

```python

# Application definition

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'rest_framework',
]
```

From here we can follow the Example look at using REST framework to build a simple API.

Since Django is single configuration, REST_FRAMEWORK is also a dictionary we can keep global settings.
In settings.py


    ```python
    # REST framework
    REST_FRAMEWORK = {
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.DjangoModelPermissionsOrAnonReadOnly'
        ]  
    }

    ```

Taking a pause, let's understand what we just did and why.
We first included the rest_framework in the settings module. 
This is because settings.py is the configuration settings file to tell django how things work.

Then we added the REST_FRAMEWORK dictionary to global settings.py also. 
These configurations allow read-only access to unauthenticated users. 
This is the only restriction added to our API at this time. 



From here, I want to jump to a quick setup found in the quickstart tutorial on the framework site.
Since we are doing a review, and this is mostly for learning, 
I won't set up a real database. Check out [this] blog post where I set up a testing environment with django and use 
postgresql as the db. For now, we stay with the default db, SQLite.

[commands][/insecure_blog]
```python 
    python3.8 manage.py migrate
```
 
Then we create an admin user to authenticate with later. For this example, I will use custom credentials. 
Feel free to follow along with quickstep. 

NOTE: If you follow the quickstep usage for password, you will be warned that the password is too common. 
You can bypass the security risk and accept the password. 


Before I jump into more coding, I want to check out the set-up by running the application. 

    ```python
    python3.8 manage.py runserver
    ```

visit: [localhost:8000] and [localhost:8000/admin]
If you see 'The installation worked successfully! Congratulations!' the application is set up correctly.

So far, we just created a project environment. We need an application. Projects are a collection of configurations and applications.
Applications are what does something. A project can contain multiple apps, and an app can be *in* multiple projects.


Next, we are going to code up a way to control the APIs output responses. To do this, we use the provided Serializer class. 
But first we need to create our app!

In path[/insecure_blog/], same directory as manage.py:

```python
    django-admin startapp blog
```

Use whatever app name you wish. The tutorial for quickstart uses `quickstart` as the app's name.

Change into the blog directory and create the module `seralizers.py`.

After that, create the views.py inside the blog directory.


Now it is time to wire up the API URLS in urls.py of the insecure_blog directory.

Finally, lets add the pagination to control how many objects per page are returned.

Now we can test these settings. Start the server again.

Okay, so we set up a basic API that we can access via the browser or via the command line using curl or httpie.
Now we examine the third-party packages. Specifically, the authentication packages.

First is the Django OAuth Toolkit which uses the OAuthLib for RFC [5842], [6749] compliance. 
[https://django-oauth-toolkit.readthedocs.io/en/latest/]

For this part, we jump from the framework tutorial to the Django OAuth Toolkit tutorial.

[breakout]
I ran into an issue at this point. It turns out that oauth2 requires some knowledge prior to setting up.



To follow along, we first install `django-oauth-toolkit` and follow the setup instructions.
This example will be using the path module inside urls.py

NOTE: don't forget to use your virtualenv if you've exited it

While I won't be creating a new project, I will be adding the   `users` app so follow that part.

Also note that on the part where they use users.User, I will be using auth.User.



```

    python3.8 -m pip install django-oauth-toolkit

```


[REVIEW]

Overall, the level of documentation for building an application using Django REST framework is astounding.
You can find docs for just about anything you wish to accomplish. If the documentation is not enough or is lacking,
then users can utilize either IRC or Stack Overflow where they can find support or even corner case problems.

What is really amazing is how easy it is to jump from development to research and back without the need for entering
tutorial hell. As show here, we utilized 3 different tutorials: Django, Django REST Framework and Django OAuth Toolkit.






