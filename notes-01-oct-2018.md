# python-notes - 01-oct-2018


### 1 - List

```python
mylist  = [ x for x in range(3) ]
```

### 2 - Generator List

```python
mygenerator = ( x for x in range(3) )
```

### 3 - Yeild list from function

```python
def createGenerator()
  mylist = range(3)
  for i in mylist:
    yield i*i

mygenerator = createGenerator()
```

### 4 - *args, \**kwargs 

We use *args when we aren’t sure how many arguments are going to be passed to a function, or if we want to pass a stored list or tuple of arguments to a function. 
\**kwargs is used when we don’t know how many keyword arguments will be passed to a function, or it can be used to pass the values of a dictionary as keyword arguments. The identifiers args and kwargs are a convention, you could also use *bob and \**billy but that would not be wise.

```python
def myFun(arg1, *argv): 
    print ("First argument :", arg1) 
    for arg in argv: 
        print("Next argument through *argv :", arg) 
  
myFun('Hello', 'Well', '2', 'SEe') 
```

```python
def myFun(arg1, **kwargs):  
    for key, value in kwargs.items(): 
        print ("%s == %s" %(key, value)) 
  
# Driver code 
myFun("Hi", first ='second', mid ='third', last='First')     
```

### 5 - Random Shuffle

```python
from random import shuffle
x = ['Keep', 'The', 'Blue', 'Flag', 'Flying', 'High']
shuffle(x)
print(x)
```
### 6 - List Sort

```python
list = ["1", "4", "0", "6", "9"]
list = [int(i) for i in list]
list.sort()
print (list)
```
### 7 - Decorators

Decorators in Python are used to modify or inject code in functions or classes. Using decorators, you can wrap a class or function method call so that a piece of code can be executed before or after the execution of the original code. Decorators can be used to check for permissions, modify or track the arguments passed to a method, logging the calls to a specific method, etc.

```python
def my_decorator(func):
    def wrapper():
        print("Something is happening before the function is called.")
        func()
        print("Something is happening after the function is called.")
    return wrapper

def say_whee():
    print("Whee!")

say_whee = my_decorator(say_whee)
```
### 8 - What is PEP 8?

PEP 8 is a coding convention, a set of recommendation, about how to write your Python code more readable. 

### 9 - Counter
```python
from collections import Counter 
c=Counter(['a','b','c','a','b','a']) 
c
```
### 10 - Print directory listings recursively
```python
def print_directory_contents(sPath):
    import os                                       
    for sChild in os.listdir(sPath):                
        sChildPath = os.path.join(sPath,sChild)
        if os.path.isdir(sChildPath):
            print_directory_contents(sChildPath)
        else:
            print(sChildPath)
```
### 11 - Module import location in python code

Module importing is quite fast, but not instant. This means that:

* Putting the imports at the top of the module is fine, because it's a trivial cost that's only paid once.
* Putting the imports within a function will cause calls to that function to take longer.

### 12 - Module import caching

* Module import are cached everytime they are imported; so it does not go through the whole import process again
* If import is inside a function; it's only imported when the function is run

### 13 - Classes are objects in Python

* While creating a class, a object of same is created.
* This object can be passed as argument, assigned to variables, attributes can be added or deleted from it and all other stuff that is supported for objects.
* Classes can be created dynamically.
* This object (the class) is itself capable of creating objects (the instances), and this is why it's a class.

```python
class ObjectCreator(object):
    pass
print ObjectCreator()
print ObjectCreator
```