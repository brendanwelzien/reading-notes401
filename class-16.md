# Intro to DJANGO
- Django is a Python-based framework
- It is an open source, but has issues with the funding and contribution

- *Django* enables development of websites
    - manages the hassle of web development, you can focus on writing your app without needing to "reinvent the wheel"
    - helps you write software that is *complete*, *versatile*, *secure*, *scalable*, *maintainable* and *portable*
## Where did it come from?
- initally developed between 2003 - 2005 where the code has turned into a generic web development framework
- Does it avoid the problems of regular platforms?
    - it supports big companies like Instagram, so it must be useful!
## What does the code look like?
- traditionally, a web application waits for *HTTP* requests from the browser, and when the request is received the application works what is needed based on the *URL* and in **POST** and **GET** data
- it then reads or writes information from a DB and then returns a response to the web browser

**URLS:** more maintainable to write a functon to *handle each resource*
    - a URL mapper is used to redirect HTTP requests to the appropriate view based on the request URL an can match patterns of strings or digits that are present in an URL and pass into a function as data
**View:** this is a request handler function, which takes HTTP requests and return HTTP responses.
    - accesses data needed to meet requests via *models*, and formats the response as *templates*
**Models:** Models are Python objects that define structure of an app's data, and provides mechanisms to manage (add, modify, delete) and query records in DB
**Templates:** this is a text file that defines the structure or layout of a file with *placeholders* used to represent the *actual content*
    - a **View** can dynamically create an HTML page using an HTML template, giving it data from a **model**.

## Django Models
- Django web apps access and manage data through Python objects which are referred as *models*
    - *models* define the **structure** of stored data, including field types, options, forms, etc.
    - no need to speak to a DB, just write the model structure and other code and DB communication is done by Django

## LocalLibrary Models
1. When designing your models make sure you have models separated for every *object (group of related info)*
    - for example, if you were storing books you would want objects for *books*, *book instances*, *authors*
    - may also want models for *selection-list options*(drop-down list, for book genre, language, etc.)
2. Once decided which models and field, think about the **relationships**
    - Django relationships allow you to use *OneToOneField*, *OneToMany(ForeignKey)*, and *ManyToManyField*

3. Models defined in *models.py* file
- example from mozilla

```python
from django.db import models

class MyModelName(models.Model):
    """A typical class defining a model, derived from the Model class."""

    # Fields
    my_field_name = models.CharField(max_length=20, help_text='Enter field documentation')
    ...

    # Metadata
    class Meta:
        ordering = ['-my_field_name']

    # Methods
    def get_absolute_url(self):
        """Returns the url to access a particular instance of MyModelName."""
        return reverse('model-detail-view', args=[str(self.id)])

    def __str__(self):
        """String for representing the MyModelName object (in Admin site etc.)."""
        return self.my_field_name
```
4. *Field* arguments
```python
my_field_name = models.CharField(max_length=20, help_text='Enter field documentation')
```
    - help text
    - verbose_name
    - default
    - null
    - blank
    - choices
    - primary_key
5. *Field Arguments*
    - CharField
    - TextField
    - IntegerField
    - DateField and DateTimeField
    - EmailField
    - FileField and ImageField
    - AutoField
    - ForeignKey
    - ManyToManyField
6. *Metadata*
    - you can declare by creating a class
    - one of the most useful features for Meta is to control the **ordering** of records when queried

```python
Class Meta:
    ordering = ['title', '-publishedDate']
```
7. Model Management
- once defined the model classes you can manipulate them to do as you would like

a. create a new record by making an instance of the model and saving it
    - `create_record = MyModelName(my_field_name="instance")`
    - `create_record.save()`
b. searching for records
    - use `objects.all()`
# Django Forms
- forms in HTML form require the `<form>` tag, which contains at least one `<input>` element of the `type="submit"`
```html
<form action="/team_name_url/" method="post">
    <label for="team_name">Enter name: </label>
    <input id="team_name" type="text" name="name_field" value="Default name for team.">
    <input type="submit" value="OK">
</form>
```
- the name and id of the field are used to identify the field in JS/CSS/HTML

*action* --> the resource/URL where data is sent for processing the form when submitted

*method* --> the method used to send the data, *post* or *get*
    - the *post* method should always be used if the data is going to change the database's page
    - the *get* method should always be used for forms that do not change user data (like a search form)

## Django Form Handling Process
1. Display the dfault form for the first time when requested by user
    * form may contain blank fields or may come pre-populated
    * form is referred as *unbound* bc it is not associated with any user data yet
2. Receive data from a submit request and bind to form
    * binding data to form means user-entered data and any erros are available when we need to re-dsiplay the form
3. Clean / Validate data
    * cleaning is removing malicious or invalid characters and converts to proper Python types
    * validating checks that the values are appropriate for field (number vs. string)
4. if any data is *invalid*, re-display the form, this time with user values and error messages for the problem fields
5. if all data is *valid*, perform required actions (save data, send, return a search, upload a file, etc.)
6. once all actions are complete, redirect user to another page
- it would be wise to use the **Form** class, which helps perform the steps above

## Declaring a Form
```python
from django import forms
class someClassName(forms.Form):
    some_variable = forms.DateField(xxxxxx="")
```
- form fields use the `DateField` for entering data... but there are anty available for *form fields*
- the most common arguments for fields are...
**required, label, label_suffix, initial, widget, help_text, error-messages, validators, localize, and disabled**

## VALIDATION
- the easiest way to validate a single field is to override the method `clean_<fieldname>()` for the field you want to check
- example below of how to override the `renewal_date`
```python
import datetime

from django import forms
from django.core.exceptions import ValidationError
from django.utils.translation import ugettext_lazy as _

class RenewBookForm(forms.Form):
    renewal_date = forms.DateField(help_text="Enter a date between now and 4 weeks (default 3).")

    def clean_renewal_date(self):
        data = self.cleaned_data['renewal_date']

        # Check if a date is not in the past.
        if data < datetime.date.today():
            raise ValidationError(_('Invalid date - renewal in past'))

        # Check if a date is in the allowed range (+4 weeks from today).
        if data > datetime.date.today() + datetime.timedelta(weeks=4):
            raise ValidationError(_('Invalid date - renewal more than 4 weeks ahead'))

        # Remember to always return the cleaned data.
        return data
```
## URL CONFIGURATION
- URL configuration will redirect URLS with the format in *views.py*
```python
urlpatterns += [
    path('book/<uuid:pk>/renew/', views.renew_book_librarian, name='renew-book-librarian'),
]
```
## View
- view has to render form when it is first called and then re-render or process data and redirect to new page depending on *errors*
    - for a **POST**, a pattern to use is `(if request.method =='POST':)`
        - this identifies form validation requests and **GET** (using an *else* condition) to identify the initial form creation
- taken from *mozilla*
```python
import datetime

from django.shortcuts import render, get_object_or_404
from django.http import HttpResponseRedirect
from django.urls import reverse

from catalog.forms import RenewBookForm

def renew_book_librarian(request, pk):
    book_instance = get_object_or_404(BookInstance, pk=pk)

    # If this is a POST request then process the Form data
    if request.method == 'POST':

        # Create a form instance and populate it with data from the request (binding):
        form = RenewBookForm(request.POST)

        # Check if the form is valid:
        if form.is_valid():
            # process the data in form.cleaned_data as required (here we just write it to the model due_back field)
            book_instance.due_back = form.cleaned_data['renewal_date']
            book_instance.save()

            # redirect to a new URL:
            return HttpResponseRedirect(reverse('all-borrowed') )

    # If this is a GET (or any other method) create the default form.
    else:
        proposed_renewal_date = datetime.date.today() + datetime.timedelta(weeks=3)
        form = RenewBookForm(initial={'renewal_date': proposed_renewal_date})

    context = {
        'form': form,
        'book_instance': book_instance,
    }

    return render(request, 'catalog/book_renew_librarian.html', context)
```

# Custom User Model
- use a custom user model for all new Django projects

- create and navigate into a dedicated directory called accounts for our code
- install Django
- make a new Django project called config
- make a new app accounts
- start the local web server
```python
$ cd ~/Desktop
$ mkdir accounts && cd accounts
$ pipenv install django~=3.1.0
$ pipenv shell
(accounts) $ django-admin.py startproject config .
(accounts) $ python manage.py startapp accounts
(accounts) $ python manage.py runserver
```
- run *migrate* after you create the customer user

## AbstractUser vs. AbstractBaseUser
- absractbaseuser requires more work

To create the initial customer user model requires 4 steps:
1. update config/settings.py
2. create a new CustomUser model
3. create a new UserCreation and UserChangeForm
4. Update the admin
- in settings you add the `accounts` app and use the **AUTH_USER_MODEL** to tell Django to use the new custom user model in place of the built-in `User` model

- now we update the *models.py* with a new user model
```python
# accounts/models.py
from django.contrib.auth.models import AbstractUser
from django.db import models

class CustomUser(AbstractUser):
    pass
    # add additional fields in here

    def __str__(self):
        return self.username
```
- now we need new versions of the form methods, stop the server and create a *new file* in the *accounts* app called **forms.py**

--> update with... for example
```python
# accounts/forms.py
from django import forms
from django.contrib.auth.forms import UserCreationForm, UserChangeForm
from .models import CustomUser

class CustomUserCreationForm(UserCreationForm):

    class Meta:
        model = CustomUser
        fields = ('username', 'email')

class CustomUserChangeForm(UserChangeForm):

    class Meta:
        model = CustomUser
        fields = ('username', 'email')
```
- then finally you update the **admin.py**
```python
# accounts/admin.py
from django.contrib import admin
from django.contrib.auth.admin import UserAdmin

from .forms import CustomUserCreationForm, CustomUserChangeForm
from .models import CustomUser

class CustomUserAdmin(UserAdmin):
    add_form = CustomUserCreationForm
    form = CustomUserChangeForm
    model = CustomUser
    list_display = ['email', 'username',]

admin.site.register(CustomUser, CustomUserAdmin)
```

- **NOW** you can run `makemigrations` and `migrate` to create a new database that uses the customer user model
[<-- Back](README.md)