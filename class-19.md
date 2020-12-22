# JSON Web Tokens
- a JSON web token is a self-contained way for securely transmitting info between parties as a JSON object
    - signed / verified by using a key

**When to use:**
- during **authorization**
- during **information exchange** --> securely transmitting information between parties

**Structure**
- consists of three parts separated by dots
    1. Header
    2. Payload
    3. Signature
    - example --> xxxxx.yyyyy.zzzzz

### Header
- consists of the *type of token* (which is JWT) and the *signing algorithm* that is used
```python
{
    "alg": xxxxxx,
    "typ": "JWT"
}
```
### Payload
- contains the claims, which are the statements about an entity and additional data
- there are three types of claims
    1. Registered : set of predefined claims which are not mandatory but recommended to provide useful claims
    2. Public : defines at will by those using JWTs
    3. Private : custom claims created to share info between parties that agree on using them are neither registered or public
- example of a paylod
```python
{
  "sub": "1234567890",
  "name": "Chester Cheetah",
  "admin": true
}
```
### Signature
- to create the signature, you have to take encoded header, encoded payload, a secret, the algorithm specified in the header and sign it
- example
```python
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```
### Putting It Together
- the output is a three Base64-URL strings separated by dots than can be passed in HTML and or HTTP environments

# Using JWT Authentication with Django REST Framework
- JWT is an authentication strategy used by client/server apps where client is a web app using JS and some frontend framework like Angular/React/VueJS

- JWT is acquired by exchanging a user and pass for an access token and a refresh token
    - access token usually lasts 5 min or can be changed
    - refresh token usually lasts 24 hours or can be changed

### Setup
- examples taken from https://simpleisbetterthancomplex.com/tutorial/2018/12/19/how-to-use-jwt-authentication-with-django-rest-framework.html
**settings.py**
```python
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    ],
}
```
**urls.py**
```python
from django.urls import path
from rest_framework_simplejwt import views as jwt_views

urlpatterns = [
    # Your URLs...
    path('api/token/', jwt_views.TokenObtainPairView.as_view(), name='token_obtain_pair'),
    path('api/token/refresh/', jwt_views.TokenRefreshView.as_view(), name='token_refresh'),
]
```

**views.py**
```python
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework.permissions import IsAuthenticated


class HelloView(APIView):
    permission_classes = (IsAuthenticated,)

    def get(self, request):
        content = {'message': 'Hello, World!'}
        return Response(content)
```

**urls.py**
```python
from django.urls import path
from myapi.core import views

urlpatterns = [
    path('hello/', views.HelloView.as_view(), name='hello'),
]
```
### Usage
- you can use HTTPie to consume API endpoints or you can use cURL

- obtaining the token
    - *authenticate* and *obtain the token*
    - endpoint is `/api/token/` and only accepts `POST` requests
- store both *access token* and the *refresh token* on client side, usually in localStorage
    - to access the protected views on backend, you should include *access token* in header of all requests `http http://127.0.0.1:8000/hello/ "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNTQ1MjI0MjAwLCJqdGkiOiJlMGQxZDY2MjE5ODc0ZTY3OWY0NjM0ZWU2NTQ2YTIwMCIsInVzZXJfaWQiOjF9.9eHat3CvRQYnb5EdcgYFzUyMobXzxlAVh_IAgqyvzCE"`
    - you can use this for the next five minutes
    - to get a new access token, you need to use the refresh token post method