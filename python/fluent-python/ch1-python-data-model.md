# Chapter 1: The Pythonic Data Model
## How do imports work in python?
The import statement does two things. It searches for the module, and binds it to a variable in the local scope.

```python
import x
```

The above will search for a module named x and bind it to the variable x in the local scope. Modules are the basic unit of code organization in python. Any file with the `.py` extension is a module. Packages are a special type of module that have a `__path__` attribute. When a package is imported, the `__init__.py` file in the root of the package is executed.

During the search process, the import system will run a number of finders to search for modules. One such finder looks for modules in each of the paths in `sys.paths`.

### Special variables
`sys.modules`: A cache of recently imported modules, and is where the module search process begins.

`sys.paths`: A list of paths one of the finders uses to search for modules.

## What is the collections module?
A module that contains a number of specialized container datatypes.

## What are doctests?
doctests are a way of testing code by executing the examples included in the docstrings of functions.

## What is __repr__?
Python objects can implement `__str__`  and  `__repr__` methods which are invoked by `str()` and `repr()` respectively. Both methods are expected to return strings. The distinction is that the return result of `__str__` is meant to be readable, whereas the return result of `__repr__` should be unambiguous and is more often used for debugging purposes. Ideally, the return result of `__repr__` should describe how to construct the object.

## What is the % operator?
It's the string formatting operator.
```python
>>> "%s went to %s" %  ('Bogdor', 'Trogdor')
'Bogdor went to Trogdor'
```