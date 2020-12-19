# Django for APIs
DJango REST framework works to create web APIs
    - you cannot build a web API with *only* DJango REST framework, it needs to be added to a project *after* Django itself has been installed
    - Django creates websites containig webpages, while DJango REST framework creates web APIs which are *a collection of url endpoints containing HTTP verbs that return JSON*

## Traditional Django
- make a directory on computer to store the code
- make directory for `library`, install `Django`, enter `virtual environment`
- run `migrate`

## First App
**App Contents** after  doing `python manage.py startapp appname`
Each app has a __init__.py file identifying it as a Python package. There are 6 new files created:

- admin.py is a configuration file for the built-in Django Admin app
- apps.py is a configuration file for the app itself
- the migrations/ directory stores migrations files for database changes
- models.py is where we define our database models
- tests.py is for our app-specific tests
- views.py is where we handle the request/response logic for our web app
- add a urls.py to handle *request/response* logic for app

1. go to `settings.py` add the new `app` to `INSTALLED_APPS`, to local
2. run `python manage.py migrate` // possibly use `makemigrations` as well

## Models
3. open up `appName/models.py`
example
```python
# books/models.py
from django.db import models

class Book(models.Model):
    title = models.CharField(max_length=250)
    subtitle = models.CharField(max_length=250)
    author = models.CharField(max_length=100)
    isbn = models.CharField(max_length=13)

    def __str__(self):
        return self.title
```
4. `python managepy makemigrations appName`
5. `python manage.py migrate`
## Admin
6. create a superuser and update `admin.py` so the appName is displayed
    7. `python manage.py createsuperuser`
8. update appName in `admin.py`
```python
# books/admin.py
from django.contrib import admin
from .models import Book

admin.site.register(Book)
```
9. navigate to `http://127.0.0.1:8000/admin` and login
10. click on `+Add` link next to `appName`

## Views
- the views.py file controls *how* DB model content is displayed
11. Update to your liking the `appName/views.py` file
```python
# books/views.py
from django.views.generic import ListView
from .models import Book


class BookListView(ListView):
    model = Book
    template_name = 'book_list.html'
```
- what still remains: make template and configure URLS

## URLs
- setup project level `urls.py` file and then one within `appName` app
12. go to `config/urls.py` and add `include` import and then a *new path for the `appName` app*
```python
# config/urls.py
from django.contrib import admin
from django.urls import path, include # new

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('books.urls')), # new
]
```
13. make sure you have a `appName/urls.py` file for urls
14. now update the file
```python
# books/urls.py
from django.urls import path

from .views import BookListView

urlpatterns = [
    path('', BookListView.as_view()),
]
```
15. final step is to create template file that controls layout of the web page
- create `templates` folder with all of the .html assets
16. now update the template file
```python
<!-- books/templates/books/book_list.html -->
<h1>All books</h1>
{% for book in object_list %}
  <ul>
    <li>Title: {{ book.title }}</li>
    <li>Subtitle: {{ book.subtitle }}</li>
    <li>Author: {{ book.author }}</li>
    <li>ISBN: {{ book.isbn }}</li>
  </ul>
{% endfor %}
```
- should now have a functional webpage for traditional Django

# Django REST Framework
- added like any other third-party app
- make sure to quit the server
- add by using pip or poetry ... `install djangorestframework~=3.11.0`
17. add to `INSTALLED_APPS` in `settings.py` file
    - make as `#3rd party`
18. an API will need a new URL route, a new view, and a new serializer file
- an approach would be to create an `api` app
- `python manage.py startapp api` (within library directory)
19. add to `INSTALLED_APPS` the `api` app
- the `api` app will not have its own DB models so no need to create a migratoin file and run migrate to update the db
20. `include` the `api` app and configure its URL route which will be `api/`
```python
# config/urls.py
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/', include('api.urls')), # new
    path('', include('books.urls')),
]
```
21. create a `urls.py` file within `api` app
- `touch api/urls.py`
- update by ....
```python
# api/urls.py
from django.urls import path
from .views import BookAPIView

urlpatterns = [
    path('', BookAPIView.as_view()),
]
```
22. move to `views.py` which relies on REST framework
- within `views.py` update to something like this...
```python
# api/views.py
from rest_framework import generics

from books.models import Book
from .serializers import BookSerializer


class BookAPIView(generics.ListAPIView):
    queryset = Book.objects.all()
    serializer_class = BookSerializer
```
- the steps required in view is to specify the `queryset` which in this case is all books, and then the `serializer_class` which is `BookSerializer`
## Serializer
- a serializer translates data into a format that is easy to digest over the internet, usually in JSON and is displayed at an API endpoint
23. make a `serializers.py` file within `api` app
- `touch api/serializers.py`
```python
# api/serializers.py
from rest_framework import serializers

from books.models import Book


class BookSerializer(serializers.ModelSerializer):
    class Meta:
        model = Book
        fields = ('title', 'subtitle', 'author', 'isbn')
```
- we extend REST framework of model to book class that specifies the model `Book` and db fields
## cURL
- we want to see what the api endpoint looks like and that it should return JSON at the url `http://127.0.0.1:8000/api/
- `python manage.py runserver`
- use the `cURL` program to execute HTTP requests via command line... For a `GET` request specify the `curl` and the `URL` we want to call
```python
$ curl http://127.0.0.1:8000/api/
[  
   {  
      "title":"Django for Beginners",
      "subtitle":"Build websites with Python and Django",
      "author":"William S. Vincent",
      "isbn":"978-198317266"
   }
]
```
- the data is here, in JSON format, but is poorly formatted, but Django provides a visual mode for API endpoints
## Browsable API
- with the local server running.. navigate to `http://127.0.0.1:8000/api/`
- the Django REST framework provides the visualization by default
- this is what raw JSON from API endpoint looks like


[<-- Back](README.md)