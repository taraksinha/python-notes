# 15-oct-2018

### 12 - making objects callable

```python
class Adder:
  def __init__(self,n):
    self.n = n
    
  def __call__(self, x ):
    return self.n + x 

>>> plus_3 = Adder(3)
>>> plus_3(4)
7

>>> callable(plus_3)
True
```


### 11 - del

```python
def yell(text):
  return test.upper() + "!"

yell('hello')

bark = yell

bark('woof')

del yell

yell('hello?')
>>NameError blah

bark('hey')
>>Still works!

bark.__name__
>>'yell'

```

### 10 - String formatting

```python

>>> "Hello, %s" % name
>>> "%x" % errno
>>> "%s %x" % ( name, errno )
>>> "%(name)s, %(errno)x" % { "name" : name , "errno" : errno }

>>> 'Hello, {}'.format(name)

>>> 'Hey {name} 0x{errno:x} error '.format(name=name, errno=errno)

>>> f'Hello, {name}!'
>>> f'{5+5}'
```
```python
from string import Template
t = Template('Hey, $name!')
t.substitute(name=name)
```

- Template Strings avoid security issues



### 9 - var_ ( underscore after the name)

- Avoid clashes with keywords, convention

### 8 - _ ( don't care about it, it's underscore)

```python
for _ in range(10):
  print _
```

```python
color, _ , _ , mileage = car
```

```python
>>> list()
[]
>>> _.append(1)
>>> _.append(2)
>>> _
[1,2]
```


### 7 - __bam__ dunder bam

```python
class PrefixPostfixTest:
  def __init__(self):
    self.__bam__ = 42

>>> PrefixPostfixTest().__bam__

### 6 - __baz is name-mangled by python interpreter

- Happens both to methods and attributes
- Probably helps in keeping clashes out of the class heirarchy tree

```python
class Test:
  def __init__(self):
    self.foo = 11
    self._bar = 23
    self.__baz = 42

dir(Test())
```

```python
class ManglingTest:
  def __init__(self):
    self.__mangled = 'hello'
    
  def get_mangled(self):
    return self.__mangled
```

```python
class MangledMethod:
  def __method(self):
    return 42
    
  def call_it(self):
    return self.__method()
```

```python
_MangledGlobal__mangled = 23

class MangledGlobal:
  def test(self):
    return __mangled

>>> MangledGlobal().test()
23
```


### 5 - wildcard imports and underscore

```python
>>> from my_module import *
>>> external_func()
23
>>> _internal_func()
NameError: "name '_internal_func' is not defined"
```

### 4 - contextlib to create with interface, generator based

```python
from contextlib import contextmanager

@contextmanager
def managed_file(name):
  try:
    f = open(name,'w')
    yield f
  finally:
    f.close()

>>> with managed_file('hello.txt') as f:
      f.write('helloworld')
      f.write('be now')
```


### 3 - try except finally ~~ with

```python
some_lock = threading.Lock()

#Harmful
some_lock.acquire()
try:
  #Do something
finally:
  some_lock.release()

#Better
with some_lock:
  #Do something
```

### 2 - Context With

```python
class ManagedFile:
  def __init__(self,name):
    self.name= name
  
  def __enter__(self):
    self.file = open(self.name,"w")
    return self.file
    
  def __exit__(self,exc_type, exc_val , exc_tb):
    if self.file:
      self.file.close()

with ManagedFile('hello.txt') as f:
  f.write('hello world')
  f.write('bye now')
```


### 1 - assertions

- Assertions can be disabled globally, so don't use them for any real validations
- Assertions are good way to handle the remaining if-elif-else condition
- Assertions are to check internal consistencies, and cannot be handled
- assert <assert condition>