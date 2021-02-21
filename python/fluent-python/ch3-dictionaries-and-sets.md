# Chapter 3: Dictionaries and Sets
## What is \_\_main\_\_?
https://docs.python.org/3/library/__main__.html

When a module is run as a script, it's name is set to `__main__`. This allows for code to be executed when the module is run directly but not when imported using the following pattern:
```python
if __name__ == '__main__':
  print('hello world')
```

## What is the distinction between __new__() and __init__()?
`__new__` takes a class argument, handles object creation and returns a new instance.  `__init__` takes an object instance of a class as an argument and handles object initialization. See [1] for more details.

```python
class Foo:
    def __new__(cls):
        print("Calling __new__ from %s" % (cls.__name__))
        return super().__new__(cls)

    def __init__(self):
        print("Calling __init__ from %s" % (self.__class__.__name__))
    
    def __str__(self):
        return "An instance of %s" % (self.__class__.__name__)

if __name__ == '__main__':
    print(Foo())
```
```python3
Calling __new__ from Foo
Calling __init__ from Foo
An instance of Foo
```

## What does the \_\_pycache\_\_/ folder contain?
A folder that contains various artifacts such as python bytecode to speed up the time it takes for a program to start.

## What is a metaclass?
```python
class Thing:
  def speak(self):
    print("I am an instance of class %s" % self.__class__.__name__)

Foo = type(
  'Foo', 
  (Thing,), 
  {
    'attr': 100,
    'add_1': lambda x: x.attr + 1
  }
)

Bar = type(
  'Bar',
  (Thing,),
  {
    'attr': 100,
    'square': lambda x: x.attr * x.attr
  }
)
```
```python3
>>> bar = Bar()
>>> bar.square()
10000
>>> bar.speak()
I am an instance of class Bar
>>> foo = Foo()
>>> foo.add_1()
101
>>> foo.speak()
I am an instance of class Foo
```

`type()` allows us to dynamically construct classes. It takes three arguments: the name of the class, the base classes to inherit from, and a dictionary containing the definitions for the class.

Metaclasses in effect allow us to override the object instantiation process.
```python
class MyMetaclass(type):
    def __new__(cls, name, bases, dct):
        print("Calling __new__ of MyMetaclass")
        obj = super().__new__(cls, name, bases, dct)
        obj.attr = 27
        return obj

class Foo(metaclass=MyMetaclass):
    def __new__(cls):
        print("Calling __new__ of Foo")
        return super().__new__(cls)

if __name__ == '__main__':
    foo = Foo()
    print(foo.attr)
    
    print(Foo.__base__)
    print(MyMetaclass.__base__)
```
```python3
Calling __new__ of MyMetaclass
Calling __new__ of Foo
27
<class 'object'>
<class 'type'>
```

Interestingly, the linter complained that the `foo` object does not have an `attr` attribute.

## What is an ABC?
https://docs.python.org/3/library/abc.html

ABC stands for abstract base class. Abstract base classes can define a set of abstract methods that inheriting classes must implement.

The `abc` module provides facilities for defining abstract base classes. One can define an abstract base class by defining a class that inherits from `ABC`, and define methods that inheriting classes must implement using the `abstractmethod` decorator.
```python
from abc import ABC, abstractmethod
from math import pi

class Shape(ABC):
    @abstractmethod
    def perimeter(self):
        pass

    @abstractmethod
    def area(self):
        pass

class Square(Shape):
    def __init__(self, side):
        self.side = side
    
    def perimeter(self):
        return 4 * self.side

    def area(self):
        return self.side * self.side

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    
    def perimeter(self):
        return 2 * pi * self.radius
    
    def area(self):
        return pi * self.radius * self.radius
```
```python3
>>> square = Square(4)
>>> square.perimeter()
16
>>> square.area()
16
>>> circle = Circle(3)
>>> circle.perimeter()
18.84955592153876
>>> circle.area()
28.274333882308138
```


## What is a PEP?
https://www.python.org/dev/peps/pep-0001/

PEP stands for python enhancement proposal. It's intended to be a design document that outlines a new feature for Python.

## References
[1] https://spyhce.com/blog/understanding-new-and-init

[2] https://realpython.com/python-metaclasses/

[3] https://www.geeksforgeeks.org/abstract-classes-in-python/

[4] https://www.python-course.eu/python3_abstract_classes.php
