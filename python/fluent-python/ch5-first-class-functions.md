# Chapter 5: First Class Functions

## What is the `lambda` keyword?
A keyword for creating anonymous functions. The body of the lambda function can only include expressions (no assignments, conditionals, loops, etc.).
```python
>>> square = lambda x: x * x
>>> add_1 = lambda x: x + 1
>>> items = [i for i in range(11)]
>>> list(map(square, items))
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
>>> list(map(add_1, items))
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]
```

## What exactly are generator functions?
Generator functions are functions that use a yield keyword to produce values lazily. Suppose we have the following classes:
```python
class LinkedListNode:
    def __init__(self, value: int):
        self.value = value
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None
    
    def insert(self, value: int):
        node = LinkedListNode(value)
        node.next = self.head
        self.head = node
    
    def __str__(self):
        values = []
        current = self.head
        while current != None:
            values.append(current.value)
            current = current.next
        
        return ' -> '.join(map(str, values))

    def __iter__(self):
        return LinkedListIterator(self.head)
```

One way to make our `LinkedList` class iterable is by implementing an iterator.
```python
class LinkedListIterator:
    def __init__(self, head: LinkedListNode):
        self.current = head
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.current == None:
            raise StopIteration()
        ret = self.current.value
        self.current = self.current.next
        return ret
```
```python
>>> for i in range(1, 6)[::-1]: l.insert(i)
... 
>>> print(l)
1 -> 2 -> 3 -> 4 -> 5
>>> for x in l: print(x)
... 
1
2
3
4
5
```

Alternatively, we can write a generator function that yields values for us.
```python
def traverse_list(l):
    current = l.head
    while current != None:
        yield current.value
        current = current.next
```
```python
>>> l = LinkedList()
>>> for i in range(1, 6)[::-1]: l.insert(i)
... 
>>> for x in traverse_list(l): print(x)
... 
1
2
3
4
5
```

## What is the `dir` function?
When called without an argument it will list the names available in the current local scope. Given an object it will attempt to return a list of attributes of that object.
```python
>>> dir()
['__annotations__', '__builtins__', '__doc__', '__loader__', '__name__', '__package__', '__spec__']
>>> from random import shuffle
>>> dir()
['__annotations__', '__builtins__', '__doc__', '__loader__', '__name__', '__package__', '__spec__', 'shuffle']
>>> def func(x): return x + 1
... 
>>> dir()
['__annotations__', '__builtins__', '__doc__', '__loader__', '__name__', '__package__', '__spec__', 'func', 'shuffle']
>>> dir(func)
['__annotations__', '__call__', '__class__', '__closure__', '__code__', '__defaults__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__',
 '__ge__', '__get__', '__getattribute__', '__globals__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__kwdefaults__', '__le__', '__lt__', '__module__',
'__name__', '__ne__', '__new__', '__qualname__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__']
```

## What is a closure?
A closure can be thought of as a function plus it's environment. In the following example we define a `make_greeter` function that takes a single `name` parameter and returns a function. Observe that after the `make_greeter` returns, the returned `greeter` function still has access to the `name` parameter passed to `make_greeter`. The function `greeter` together with a variable binding that includes `name` forms a closure.

```python
def make_greeter(name):

    def greeter():
        print("Hello %s!" % (name))

    return greeter
```
```python
>>> foo_greeter = make_greeter("foo")
>>> foo_greeter()
Hello foo!
>>> bar_greeter = make_greeter("bar")
>>> bar_greeter()
Hello bar!
```

## What is WSGI?
WSGI stands for web server gateway interface. It is a standard that specifies how web servers can call python web application code. There are two sides that need to be implemented: the web server side, and the web application side (implemented by the python web framework).

A web server passes requests to the WSGI container running the application.

## References
[1] https://wiki.python.org/moin/Generators

[2] https://zetcode.com/python/python-closures/

[3] https://en.wikipedia.org/wiki/Closure_(computer_programming)

[4] https://www.fullstackpython.com/wsgi-servers.html