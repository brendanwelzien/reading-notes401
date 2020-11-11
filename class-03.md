# FileIO and Exceptions

## Reading and Writing Files in Python
One of the more common tasks Python utilizes is reading and writing files.

*What is a file?*
- a file is a compilation of bytes used to store data and is stored in a specific format
    1. Header: metadata about contents of file (name, size, type, etc.)
    2. Data: contents of file as written by creator
    3. End of File (EOF): special character that indicates end of file

*File Paths*
- When you access a file, a file path is required. The file path is a string that represents the file's location and is broken up into parts
    1. Folder path: the file folder location where subsequent folders are separated by forward slash
    2. File Name: name of file
    3. Extension: end of file path pre-pended with a period to indicate file type

*Character Encoding*
- a common problem is encoding of the byte data, the most common encoding are ASCII and UNICODE
    - these share the same numerical to character values, but it is important to note that parsing a file with the wrong character encoding leads to failure

*Working with Python Files*
- when you want to work with a file, you must first *open* it.. this is done by invoking **open()** built-in function
    --> file = open(somefilename.txt')
- you should always remember to *close* the file as well
    - two ways to ensuring a file is closed..
    1. use *try-finally* block
        ```python
            reader = open('dog_breeds.txt')
            try:
                # Further file processing goes here
            finally:
                reader.close()
        ```
    2. close a file with the *with* statement
    ```python
        with open('dog_breeds.txt') as reader:
    # Further file processing goes here
    ```

    - the with statement takes care of closing the file
```python
with open('dog_breeds.txt', 'r') as reader:
    # Further file processing goes here
```
- we can alter how to open a file by using *r* (reading), *w* (open for writing), *rb* or *wb* (open in binary mode (read/write using byte data))

*File types*
1. Text Files : open('bbb.txt') / open('ccc.txt', 'r' or 'w')
2. Buffered binary files : ('bbb.txt', 'rb' or 'wb')
3. raw binary files : ('bbb.txt, 'rb', buffering=0)

### Reading and Writing Opened Files
- .read(size=-1)
    - this reads based on size bytes
- .readline(size=-1)
    - this reads at most size number of characters from the line
- .readlines()
    - this reads the remaining lines from the file object and returns them as a list

<------Example------> with iteration
```python
with open('dog_breeds.txt', 'r') as reader:
   # Read and print the entire file line by line
    line = reader.readline()
    while line != '':  # The EOF char is an empty string
        print(line, end='')
         line = reader.readline()
Pug
Jack Russell Terrier
English Springer Spaniel
German Shepherd
Staffordshire Bull Terrier
Cavalier King Charles Spaniel
Golden Retriever
West Highland White Terrier
Boxer
Border Terrier
```


## Python Exceptions
A python program ends as soon as there is an error. The error can be *syntax* related or an *exception*
    - a syntax error occurs when the parser detects an incorrect statement
    - an arrow will indicate where the syntax error lies
    - an exception error occurs when syntactically Python Code results in an error
        - there are many built-in exception in Python and it will list the type
- you can use *raise* to throw an exception if a condition occurs

```python
x = 5
if x > 5:
    raise Exception('x should not exceed 5...')
```

- instead of waiting for a program to crash in the middle of its coursek, you can make an *assertion* in Python
    - we assert that if a condition is true, then the program will continue, if it is false you can let the program throw an *AssertionError* exception
- the *try* and *Except* block is used to catch and handle exceptions

    - try: run this code....
    - except: execute this code when there is an exception
    - else: no exceptions? Run this code
    - finally: always run this code

*Summary of Python Exceptions taken from realpython.com*
- raise allows you to throw an exception at any time.
- assert enables you to verify if a certain condition is met and throw an exception if it isn’t.
- In the try clause, all statements are executed until an exception is encountered.
- except is used to catch and handle the exception(s) that are encountered in the try clause.
- else lets you code sections that should run only when no exceptions are encountered in the try clause.
- finally enables you to execute sections of code that should always run, with or without any previously encountered exceptions.

[<-- Back](README.md)