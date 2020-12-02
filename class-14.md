# Web Scraping
- web scraping is a technique used to access and extract large amounts of infromation from a website which saves time and effort
    - this is automated
    1. read through a website's terms and conditions to understand whether you can legally use the data
    2. Make sure you are not downloading data too fast because it will break the website, you may be blocked

## Inspecting the Website
- inspect the page to find the links to files you want to download
    - aka *href's*
    - now that we have located the file links we want to download, head to Python
## Python Code
- start by importing libraries
```python
import requests, urllib.request, time
from bs4 import BeautifulSoup
```
- next set the URL to the website and access the site with the requests library
```python
url = 'http://some.link.html'
response = requests.get(url)
```
- if the access is successful you should see the output response

- next you need to *parse* the html with *BeautifulSoup* so that it can work with a data structure, etc.
```python
b_soup = BeautifulSoup(response.text, "html.parser")
```
- use the method `.findAll` to locate all of the `<a>` tags
    - soup.findAll('a')
    - this will give you every line of code that has the tag, andthen you want to grab what you need
- extract the link(s) that you want
```python
one_a_tag = soup.findAll('a')[38]
link = one_a_tag['href']
```
    ----> this code saves the first text file to a variable link
    ---->
[<-- Back](README.md)