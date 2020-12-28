# Configuring Django Settings: Best Practices
Common Issues:
- different environments
- sensitive data
- sharing settings between team members -- eliminating human error
- Django settings are in Python code

- there is no built-in way to configure Django settings without hardcoding

## settings_local.py
- extend all environment-specific settings
```python
ALLOWED_HOSTS = ['example.com']
DEBUG = False
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'production_db',
        'USER': 'user',
        'PASSWORD': 'password',
        'HOST': 'db.example.com',
        'PORT': '5432',
        'OPTIONS': {
            'sslmode': 'require'
        }
    }
}

...

from .settings_local import *
```
```python
ALLOWED_HOSTS = ['localhost']
DEBUG = True
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'local_db',
        'HOST': '127.0.0.1',
        'PORT': '5432',
    }
}
```
- separate settings file for *each* environment*
- settings/
    - `__init__.py`
    - `base.py`
    - `ci.py`
    - `local.py`
    - `staging.py`
    - `production.py`
        - `qa.py`

settings/local.py
```python
from .base import *


ALLOWED_HOSTS = ['localhost']
DEBUG = True
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'local_db',
        'HOST': '127.0.0.1',
        'PORT': '5432',
    }
}
```
- to run a project with *specific* configuration, you need to set additional parameter
`python manage.py runserver --settings=settings.local`
- still need to find a way to handle secret passwords and tokens
    - to solve sensitive data, use environment variables
```python
import os

from django.core.exceptions import ImproperlyConfigured

def get_env_value(env_variable):
    try:
        return os.environ[env_variable]
    except KeyError:
    error_msg = 'Set the {} env variable'.format(var_name)
    raise ImproperlyConfigured(error_msg)

SECRET_KEY = os.environ['SECRET_KEY']
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': os.environ['DATABASE_NAME'],
        'HOST': os.environ['DATABASE_HOST'],
        'PORT': int(os.environ['DATABASE_PORT']),
    }
}
```
- this handles the *KeyError* exceptions and we still need to convert types manually (use third-party)

it is important to...
- keep settings in environment variables
- write default values for production configuration (exclude *secret keys and tokens*)
- do not hardcode sensitive settings and do not put them in VCS
- split settings into groups--> Django, third-party, project
- follow naming conventions for custom (project) settings

# SSH
- Secure Shell, is a remote admin protocol that allows users to control and modify remote servers over internet

### Procedure
1. head over to terminal
2. type SSH command which is three parts
    - `ssh {user}@{host}`
    - user = account you want to access or *root* for admin
    - host = refers to computer or place you want to access like an IP or domain name
3. type in password, nothing will appear on screen

- information regarding host and client
- *host* refers to remote server you are trying to access
- *client* refers to computer you using to access host
- SSH uses 3 encryption technologies
    - symmetrical encryption
    - asymmetrical encryption
    - hashing

*Symmetric Encryption*
- where a *secret key* is used for both encryption and decryption of a message by both the client and the host
- often called a *shared key*
- process carried out by a *key exchange algorithm*
    - key is never transmitted between client and host, but the two computers share pieces of data to calculate together the secret key
*Asymmetric Encryption*
- used two separate keys for encryption and decryption (known as *public* and *private* key)
*Hashing*
- one-way hashing is never meant to be decrypted
- uses HMACs to identify authenticity of messages
    - Hash-based Message Authentication Code

### Establishing Connection
1. Both the systems must agree upon encryption standards to protect future communications
2. The user must authenticate themselves