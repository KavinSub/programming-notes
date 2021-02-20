# Chapter 2: An Array of Sequences
## What is the fluent interface?
https://en.wikipedia.org/wiki/Fluent_interface

An object oriented API whose design relies on object chaining.

## How does Timsort work?
At a high level, Timsort combines merge sort and insertion sort. It's designed to take advantage of ordered contiguous subsequences that may already exist in an unsorted list. In the worst case it runs in O(n log n) time and in the best case it runs in linear time.

## What is a MemoryView?
https://docs.python.org/3/library/stdtypes.html#memory-views

### What is the buffer protocol?
https://docs.python.org/3/c-api/buffer.html#bufferobjects