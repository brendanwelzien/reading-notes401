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
