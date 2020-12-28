# Django, Building an API, REST, Docker ?
- rest requires model, views, serializers, urls
- this is API first development, so we have the correct setup for consumer use (requires building out front-end in react)
## For vanilla Django setup
- mkdir  folder (`sneakers` for example)
- cd into folder
- poetry init -n
- poetry shell
- add dependencies.. poetry add django djangorestframework --dev black flake8
- django-admin startproject app_project .
- python manage.py startapp `sneakers` (this is app name for this example)
- python manage.py `migrate`
- python manage.py makemigrations for when you change `models.py`
- touch sneakers/urls.py
- python manage.py runserver
## server is setup, jump into code now
- `models.py`in sneakers
```python
from django.db import models
from django.contrib.auth import get_user_model
class Sneaker(models.Model):
    name = models.CharField(max_length=200)
    # these can be different
    description = models.TextField(default="")
    purchaser = models.ForeignKey(get_user_model(), on_delete=models.CASCADE)
    
    def __str__(self):
    return self.name
```
- go to `settings.py` to let overall project that `sneakers` is an installed app
    - go to `INSTALLED_APPS` and add 'sneakers' (app name)
    - also add `rest_framework',` 
- python manage.py `makemigrations` sneakers to verify model was made and migrated
- python manage.py `migrate`

- go to `urls.py` in project level

```python
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/v1/sneakers/', include('sneakers.urls')),
]
```
- go to `sneakers.urls`
```python
from django.urls import path
from .views import SneakerListCreate

urlpatterns = [
    path('', SneakerListCreate.as_view(), name='sneaker_list_create'),
]
```
- go to and create `serializers.py` inside of appname folder

- serializers are responsible for turning model data into json form!

```python
from .models import Sneaker
from rest_framework.serializers import ModelSerializer

class SneakerSerializer(ModelSerializer):
    class Meta:
        model = Sneaker
        # what fields do we want to expose for JSON?
        fields = ("id", "name", "purchaser", "description") # need to be in model and need to match
```
- go to `views.py` in app
```python
from django.shortcuts import render
from rest_framework.generics import ListCreateAPIView, RetrieveUpdateDestroyAPIView
from .models import Sneaker
from .serializers import SneakerSerializer

class SneakerListCreate(ListCreateAPIView):
    queryset = Sneaker.objects.all() # doesnt always need to be all if you want to filter
    serializer_class = SneakerSerializer 
class SneakerRetrieveUpdateDestroy(RetrieveUpdateDestroyAPIView):
    queryset = Sneaker.objects.all()
    serializer_class = SneakerSerializer
```
- almost at full crud, now we need to connect the CRUD to urls
- users get created by administrator.. so login to /admin after creating a `python manage.py createsuperuser` and `python manage.py runserver`
- go to`urls.py` in sneakers

```python
django.urls import path
from .views import SneakerListCreate, SneakerRetrieveUpdateDestroy

urlpatterns = [
    path('', SneakerListCreate.as_view(), name='sneaker_list_create'),
    path('<int:pk>/', SneakerRetrieveUpdateDestroy.as_view(), name='sneaker_retrieve_update_destroy'),
]
```
- go to server route `api/v1/sneakers/` and check for CRUD

-  now go to `settings.py` and add *permissions* classes after STATIC_URL
```python
REST_FRAMEWORK = {
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.IsAuthenticated',
    ],
}
```
- prove the authentication by going into the admin panel, login, view site at /api/v1/sneakers/ and the top right should say for now the superuser's name
- go back to admin and add user, pass, confirmation, then go back to view site at /api/v1/sneakers/1/
    - we do not at this time have ability to switch users so lets do that

- go to project `urls.py`
- add urlpattern

```python
path('api-auth/', include('rest_framework.urls')),
```
- now we have an arrow drop down on top right of user to logout and back in
- now we can add permissions on various levels of api, at a form, make it more strict, read only, etc.

- head to `permissions.py` or create if have not done yet and add permissions to class(es)
```python
from rest_framework import permissions

class IsPurchaserOrReadOnly(permissions.BasePermission):
    def has_object_permission(self, request, view, obj):
        #return super().has_object_permission(request, view, obj)
        if request.method in permissions.SAFE_METHODS:
            return True
        # purchaser must match model
        return obj.purchaser == request.user
```
- head to `views.py` to connect the permission and add this....
```python
from .permissions import IsPurchaserOrReadOnly
class SneakerRetrieveUpdateDestroy(RetrieveUpdateDestroyAPIView):
    
    queryset = Sneaker.objects.all()
    serializer_class = SneakerSerializer

    permission_classes = (IsPurchaserOrReadOnly,)
```
- user should now only be able to get / read the list and not delete or put it
- this is an example of one permission, add more if needed

## Moving to API requests

- install httpie, go to command line
- `http -h` for help
- `http localhost:8000/api/v1/sneakers/`
- it will say authenticatin credentials were not provided
    - you would have to turn off REST_FRAMEWORK in settings and reboot server, but we are NOT going to do that
- we now need to use JSON web tokens
- install django rest framework simplejwt (can grab from github)
-  poetry add `djangorestframework-simplejwt`
- need to update `settings.py` and add to list of authentication 
```python
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': (
            'rest_framework_simplejwt.authentication.JWTAuthentication',
            'rest_framework.authentication.SessionAuthentication',
            'rest_framework.authentication.BasicAuthentication',
    )
}
```
- go to project `urls.py` and add url patterns for tokens and import from library

```python
from rest_framework_simplejwt.views import (
    TokenObtainPairView,
    TokenRefreshView,
)
urlpatterns = [
    path('api/token/', TokenObtainPairView.as_view(), name='token_obtain_pair'),
    path('api/token/refresh/', TokenRefreshView.as_view(), name='token_refresh_pair'),
]
```
- go to terminal and do `http POST localhost:8000/api/token/ username=brendan password=xxxx`
- should get back some JSON with 2 keys of access and refresh tokens
- now we need to apply this for all users
- `http localhost:8000/api/v1/sneakers/ `
    - we need to pass in the token along with this request... so copy the **access** token
- `http GET localhost:8000/api/v1/sneakers/`
    - it will say credentials are needed
- now... `http GET localhost:8000/api/v1/sneakers/ Authorization: Bearer accesstokenxxxxxx`
- some other server might be running so you need to check using `docker ps -a` via its status
- `docker-compose ps` into the directory with the server that is running
- or kill it by using `docker stop NAMES value`
- check it is dead by using docker ps

- now try again running the server and performing `http GET localhost:8000/api/v1/sneakers/ Authorization: Bearer accesstokenxxxxxx`
- if token is expired... Use the refresh token or login again
    - login again by doing `http POST:8000/api/token/ username =brendan password=xxx`
    - you can configure request methods using Postman or just use httpie
    - go to authorization tab, bearer token,

- check when having docker applied
- docker -v
- docker-compose -v

## Using Docker and gunicorn for building production server
- after building and running in docker
- add `poetry add gunicorn`
- make sure requirements.txt get updated with that
- `poetry export -o requirements.txt --without-hashes`
- go into `build` of docker-compose.yml
```python
    build:
    command: gunicorn sneakers_project.wsgi:application --bind 0.0.0.0:8000 --workers 4
    # command: python/code/manage.py runserver 0.0.0.0:8000
```
- the port needs to match the `ports` section in the yml file
- now new to rebuild the docker file
- `docker-compose up --build` or `docker-compose up`
- go into httpie
- `http POST :8000/api/token/ username=brendan password=xxx`
    - now the server is running as production server and NOT DATABASE SERVER
- turn `DEBUG`: False in `settings.py`
    - now routes will show bad error bc we do not want to show front-end all of the server-creator information
