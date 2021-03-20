# Chapter 9: A Pythonic Object

## What is a use case of the bytes method?
I'm not finding a clear answer online, but I get the impression that it can be used for seralizing objects.
```python
>>> from array import array
>>> items = [1, 2, 3, 4, 5]
>>> arr_1 = array('i', items)
>>> arr_1
array('i', [1, 2, 3, 4, 5])
>>> arr_1_bytes = bytes(arr_1)
>>> arr_1_bytes
b'\x01\x00\x00\x00\x02\x00\x00\x00\x03\x00\x00\x00\x04\x00\x00\x00\x05\x00\x00\x00'
>>> arr_2 = array('i')
>>> arr_2.frombytes(arr_1_bytes)
>>> arr_2
array('i', [1, 2, 3, 4, 5])
>>> arr_1 == arr_2
True
```
## What is the property decorator?
```python
class Container:
  def __init__(self, item):
    self.__item = item

  @property
  def item(self):
    return self.__item
```
```python
>>> container = Container(27)
>>> container.__item
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'Container' object has no attribute '__item'
>>> container.item
27
>>> 
```