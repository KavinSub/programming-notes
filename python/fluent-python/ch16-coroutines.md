# Chapter 16: Coroutines

## Using the send method
### Example 1
```python
def test():
  print('Starting test')
  val = yield
  print('Received value: {}'.format(val))
```
```python
>>> gen = test()
>>> gen
<generator object test at 0x101a75190>
>>> next(gen)
Starting test
>>> gen.send(27)
Received value: 27
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```

### Example 2
This did not behave how I guessed it would, but illustrative nonetheless.
```python
def adder():
  print('Starting Adder')
  executing = True
  while executing:
    msg = yield
    if msg == 'exit':
      executing = False
    else:
      a, b = msg
      yield a + b
  print('Stopping Adder')
```
```python
>>> add_coroutine = adder()
>>> dir(add_coroutine)
['__class__', '__del__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', '__le__', '__lt__', '__name__', '__ne__', '__new__', '__next__', '__qualname__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'close', 'gi_code', 'gi_frame', 'gi_running', 'gi_yieldfrom', 'send', 'throw']
>>> add_coroutine.gi_running
False
>>> next(add_coroutine)
Starting Adder
>>> add_coroutine.send(2, 3)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: send() takes exactly one argument (2 given)
>>> add_coroutine.send((2, 3))
5
>>> add_coroutine.send((1, 10))
>>> next(add_coroutine)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/Users/kasubram/Sandboxes/fluent-python/ch16/example_2.py", line 9, in adder
    a, b = msg
TypeError: cannot unpack non-iterable NoneType object
>>> next(add_coroutine)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```

## What is the Tornado library?
https://www.tornadoweb.org/en/stable/
