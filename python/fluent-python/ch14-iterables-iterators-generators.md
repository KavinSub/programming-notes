# Chapter 14: Iterables, Iterators, and Generators

## A Bad Sequence
I was curious how python uses the `__len__` and `__getitem__` methods to implement sequence behavior, so I implemented a bad sequence class that returns the index if it's 0 or 2, but raises an IndexError otherwise.
```python
class BadSequence:
  def __len__(self):
    return 2
  
  def __getitem__(self, index):
    if index == 0 or index == 2:
      return index
    else:
      raise IndexError()
```
```
>>> seq = BadSequence()
>>> for i in seq: print(i)
... 
0
```
It looks like the behavior is to try calling `__getitem__` with index 0 and keep incrementing until it catches an IndexError exception.