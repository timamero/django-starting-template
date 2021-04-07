# Django Starting Template
Instructions to create a skeleton Django website with a home page.

Using:
* Windows
* VS Code
* Python 3.9.1

## Instructions

### Set up Django Environment
1. Create virtual environment
    ```
    py -3.9 -m venv venv
    ```
    * [Check Python version that you can use with Django](https://docs.djangoproject.com/en/3.1/faq/install/)  

2. Go into project folder and start Django project
    ```
    django-admin startproject project_name .
    ```
    * [startproject](https://docs.djangoproject.com/en/3.1/ref/django-admin/#startproject) (Django Docs)

3. Create Django app
    ```
    py manage.py startapp app_name
    ```
    * [startapp](https://docs.djangoproject.com/en/3.1/ref/django-admin/#startapp) (Django Docs)

4. Set up database
    * If using SQLite, no additional configuration or setup is required
    * [Databases](https://docs.djangoproject.com/en/3.1/ref/databases/) (Django Docs)

5. Register application
    * Open settings.py and add application to `INSTALLED_APPS`
    ```
    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'app_name',
    ]
    ```
    * [Applications](https://docs.djangoproject.com/en/3.1/ref/applications/) (Django Docs)

6. Change time zone
    * In settings.py update `TIME_ZONE` to your time zone
    ```
    TIME_ZONE = 'America/Los_Angeles'
    ```
    * [Default time zone and current time zone](https://docs.djangoproject.com/en/3.1/topics/i18n/timezones/#default-time-zone-and-current-time-zone) (Django Docs)

### Configure URL Mappings
1. Open urls.py (in same folder as settings.py) and add paths from application
    ```
    from django.urls import include

    urlpatterns += [
        path('app_name/', include('app_name.urls')),
    ]
    ```
    * [path](https://docs.djangoproject.com/en/3.1/ref/urls/#path) (Django Docs)
    * [include](https://docs.djangoproject.com/en/3.1/ref/urls/#include) (Django Docs)

2. Enable the serving of static files by adding the following to urls.py
    ```
    # Add url mapping to serve static files during development
    from django.conf import settings
    from django.conf.urls.static import static

    urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
    ```
    * [Serving static files during development](https://docs.djangoproject.com/en/3.1/howto/static-files/#serving-static-files-during-development) (Django Docs)

3. Create a file in the application folder called urls.py (app_name/urls.py) and add the following
    ```
    from django.urls import path
    from . import views

    urlpatterns = [

    ]
    ```

### Run Database Migrations
```
py manage.py makemigrations
py manage.py migrate
```
* [Migrations](https://docs.djangoproject.com/en/3.1/topics/migrations/) (Django Docs)

### Create Superuser
* Superuser will have access to admin site
```
py manage.py createsuperuser
```
* [createsuperuser](https://docs.djangoproject.com/en/3.1/ref/django-admin/#createsuperuser) (Django Docs)

### Test admin site
```
py manage.py runserver
```
* Go to admin site at http://127.0.0.1:8000/admin
* Test log in
* [The Django admin site](https://docs.djangoproject.com/en/3.1/ref/contrib/admin/) (Django Docs)

### Create the index page
1. Open app_name/urls.py and add the following to `urlpatterns`
    ```
    urlpatterns = [
    path('', views.index, name='index'),
    ]
    ```
2. Open app_name/views.py and add the index function view
    ```
    def index(request):
        return render(request, 'index.html')
    ```
    [Writing views](https://docs.djangoproject.com/en/3.1/topics/http/views/) (Django Docs)
3. Create templates folder in the application folder.  In that folder create the file base.html which will base template for all html files. Add the following to base.html
    ```
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        {% block title %}<title>Title</title>{% endblock title %}
        {% load static %}
        <link rel="stylesheet" href="{% static 'css/styles.css' %}">
    </head>
    <body>
        <nav>
            <a href="{% url 'index' %}" class="nav-link">Home</a>
        </nav>
        <main>
            {% block content %}{% endblock content %}
        </main>
        <footer>
            <p>&#169;2021 </p>
        </footer>      
    </body>
    </html>
    ```

4. In the templates folder create the file index.html. Add the following to index.html.
    ```
    {% extends 'base.html' %}

    {% block content %}
    <h1>Site Title</h1>
    {% endblock content %}

    ```

5. Create static/css folder in the application folder . In that folder create the styles.css file.


Next steps after creating skeleton Django website:
- Create models, forms, additional views
- Add templates and styling

