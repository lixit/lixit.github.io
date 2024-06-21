---
layout: post
title: The Python Cheatsheet
---

### *Numbers*

- **int** eg. 2, 4, 20
- **float** eg. 5.0, 1.6

Division ( / ) always returns a float. // returns an integer  

### *Strings*

 ('...') or double quotes ("...") with the same result.  
The only difference between the two is that within single quotes you don’t need to escape " (but you have to escape \') and vice versa.  

raw strings  
```python
print(r'C:\some\name')  # note the r before the quote
```
multiple lines  
"""...""" or '''...'''.  

```python
print("""\
Usage: thingy [OPTIONS]
     -h                        Display this usage message
     -H hostname               Hostname to connect to
""")
```

Strings can be concatenated with the + operator. *string literals* are automatically concatenated.  

Strings can be *indexed* and *sliced*. But they cannot be changed.
```python
word[0]
word[-1]
word[2:5]
word[0] = 'J' # wrong. String cannot be changed
```

### *Lists*

a list of comma-separated values (items) between square brackets. Lists might contain items of different types.  

can be indexed ,sliced and changed. Assignment to slices is also possible. All slice operations return a new list.  
add new items at the end of the list, by using the append() method.  

The built-in function len() also applies to lists.

*multiple assignment*  
the expressions on the right-hand side are all evaluated first before any of the assignments take place. The right-hand side expressions are evaluated from the left to the right.
```python
a, b = b, a+b
```

# Control Flow Tools

### if

An if … elif … elif … sequence is a substitute for the switch or case statements found in other languages.

### for

Python’s for statement iterates over the items of any sequence (a list or a string), in the order that they appear in the sequence.
 
### The range() function
```python
range(-10, -100, -30)
  -10, -40, -70
```
In many ways the object returned by range() behaves as if it is a list, but in fact it isn’t. It is an object which returns the successive items of the desired sequence when you iterate over it, but it doesn’t really make the list, thus saving space.  
how to get a list from a range. Here is the solution:  
*list(range(4))*  

### break and continue Statements, and else Clauses on Loops

The break statement, like in C, breaks out of the innermost enclosing for or while loop.  
Loop statements may have an else clause. a loop’s else clause runs when no break occurs.  
The continue statement, also borrowed from C, continues with the next iteration of the loop.  
The pass statement does nothing.  

# Defining Functions
```python
def my_function(my_parameter):
	***A short, concise summary of the object’s purpose.
	
	one or more paragraphs describing the object’s calling conventions, 
	its side effects, etc.s
	***
	function body here
	return something
```
**Function Annotations** --Python types.  
The following example has a positional argument, a keyword argument, and the return value *annotated*  
```python
def f(ham: str, eggs: str = 'eggs') -> str:
	print("Annotations:", f.__annotations__)
	print("Arguments:", ham, eggs)
	return ham + ' and ' + eggs
```

To declare types with subtypes, use the standard Python module `typing`  
```python
from typing import List, Set, Tuple, Dict
def process_items(items: List[str], items_t: Tuple[int], items_s: Set[bytes], items_d: Dict[str, float])
	pass

```

Classes as types
```python
class Persion:
	def __init__(self, name: str):
		self.name = name
		
def get_person_name(one_person: Person):
	return one_person.name
```


**Three** forms to define functions with a variable number of arguments  
  
**Default Argument Values**  
```python
# specify a default value for one or more arguments
# The default values are evaluated at the point of function definition in the defining scope
# the default is shared between subsequent calls.
def ask_ok(prompt, retries=4, reminder='Please try again'):
```
**Keyword Arguments**
```python
def my_function(my_positional_arguments, kwarg='my_value')
```
In a function call, keyword arguments must follow positional arguments.   

```python
def cheeseshop(kind, *arguments, **keywords):

# kind receives formal parameter
# *arguments receive a **tuple**
# **keywords receive a **dictionary**
```
**Special parameters**
```python
def f(pos1, pos2, /, pos_or_kwd, *, kwd1, kwd2):
      -----------    ----------     ----------
        |             |                  |
        |        Positional or keyword   |
        |                                - Keyword only
         -- Positional only
```
# Lambda

lambda a, b: a+b

# Data Structures

*List Comprehensions*  
```python
squares = [x**2 for x in range(10)]

# create a list of 2-tuples like (number, square)
[(x, x**2) for x in range(6)]

# flatten a list using a listcomp with two 'for'
vec = [[1,2,3], [4,5,6], [7,8,9]]
[num for elem in vec for num in elem]

#Nested List Comprehensions
[[row[i] for row in matrix] for i in range(4)]
```
The **del** statement  
1. There is a way to remove an item from a list given its index instead of its value: the del statement.
2. delete a key:value pair in Directories
3. delete entire variables

**Tuples**  
A number of values separated by commas.  

Tuples are immutable, and usually contain a heterogeneous sequence of elements that are accessed via unpacking or indexing (or even by attribute in the case of namedtuples).  
Lists are mutable, and their elements are usually homogeneous and are accessed by iterating over the list.
```python
t = 12345, 54321, 'hello!'

# Tuples may be nested:
u = t, (1, 2, 3, 4, 5)

# Tuples are immutable:
# they can contain mutable objects:
v = ([1, 2, 3], [3, 2, 1])

#Empty tuples are constructed by an empty pair of parentheses;
#a tuple with one item is constructed by following a value with a comma 
empty = ()
singleton = 'hello',

#tuple packing
t = 12345, 54321, 'hello!'

#sequence unpacking
x, y, z = t

#multiple assignment is really just a combination of tuple packing and sequence unpacking.
```

**Sets**  
A set is an unordered collection with no duplicate elements.  

Curly braces or the set() function can be used to create sets. Note: to create an empty set you have to use set(), not {}; the latter creates an empty dictionary  
```python
basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'}

a = set('abracadabra')
b = set('alacazam')
a                                  # unique letters in a

a - b                              # letters in a but not in b

a | b                              # letters in a or b or both

a & b                              # letters in both a and b

a ^ b                              # letters in a or b but not both
```
**Dictionaries**  
A pair of braces creates an empty dictionary: {}. Placing a comma-separated list of key:value pairs within the braces adds initial key:value pairs to the dictionary  
```python
tel = {'jack': 4098, 'sape': 4139}
tel['guido'] = 4127
tel

tel['jack']

del tel['sape']

list(tel)

sorted(tel)

'guido' in tel

'jack' not in tel

#The dict() constructor builds dictionaries directly from sequences of key-value pairs
dict([('sape', 4139), ('guido', 4127), ('jack', 4098)])

# dict comprehension
{x: x**2 for x in (2, 4, 6)}

#When the keys are simple strings, it is sometimes easier to specify pairs using keyword arguments:
dict(sape=4139, guido=4127, jack=4098)
```
**Looping Techniques**  
when looping through dictionaries, the key and corresponding value can be retrived at the same time using the items() method.  
```python
knights = {'gallahad': 'the pure', 'robin': 'the brave'}
for k, v in knights.items():
    print(k, v)
```
when looping through a sequence, the position index and corresponding value can be retrieved at the same time using the enumerate() function.  
```python
for i, v in enumerate(['tic', 'tac', 'toe']):
    print(i, v)
```
To loop more sequences at the same time, the entries can be paired with the zip() function.  
```python
questions = ['name', 'quest', 'favorite color']
answers = ['lancelot', 'the holy grail', 'blue']
for q, a in zip(questions, answers):
    print('What is your {0}?  It is {1}.'.format(q, a))
```
To loop over a sequence in reverse
```python
for i in reversed(range(1, 10, 2)):
```
To loop over a sequence in sorted order
```python
basket = ['apple', 'orange', 'apple', 'pear', 'orange', 'banana']
for f in sorted(set(basket)):
    print(f)
```

**Modules**  
Python has a way to put definitions in a file. Such a file is called a module; definitions from a module can be imported into other modules or into the main module.  
```python
# only import module name
improt some_module

# use the module name to access the functions or the module's global variables
some_module.some_function(some_parameter)
modname.itemname

# do not import module name and import names from a module directly into the importing module's symbol table.  
from fibo import fib, fib2
fib(100)

# import all names that a module defines
from fibo import *

# impot the same way that import will do, with the only difference of it being only available as fib
import fibo as fib
fib.fib(500)

from fibo imort fib as fibonacci
fibonacci(500)

# reload the module
import importlib
importlib.reload(modulename)
```
Executing modules as scripts  
```sh
python fibo.py <arguments>
```
add this code at the end of your module
```python
if __name__ == "__main__":
	import sys
	fib(int(sys.argv[1]))
```
```sh
python fibo.py 50
```
If the module is imported, this code is not run  

**The Module Search Path**
1. first search built-in modules
2. then search in a list of directories given by the variable sys.path. sys.path initialized from:
	- The directory containing the input script.
	- PYTHONPATH (with the same syntax as the shell variable PATH)
	- The installation-dependent default.
	
After initialization, Python programs can modify sys.path. The directory containing the script being run is placed at the begginning of the search path, ahead of the standard library path.  

**"Compiled" Python files**  
only speed up loading time.  
Python caches the compiled version of each module in the "__pycache__" directory under the name module.version.pyc  
always recompiles the module that is loaded directly from the command line.  
does not check the cache if there is no source module.  

**Standard Modules**  
a library of standard modules. Some modules are built into the interpreter; these provide access to operations that are not part of the core of the language for efficiency or to provide access to operating system primitives such as system calls.  

**The dir() function**  
The built-in function dir() is used to find out which names a module defines. It returns a sorted list of strings.  
```python
import fibo
dir(fibo)

# Without arguements, dir() lists the names you have defined currently
dir()

# dir() does not list the names of built-in functions and variables. If you want a list of those, they are defined in the standard module builtins:
import builtins:
dir(builtins)
```

**Packages**

packages -> modules -> functions/variables  
When importing the package, Python searches through the directories on sys.path looking for the package subdirectory.  
The "__init__.py" files are required to make Python treat directories containing the file as packages.  

```python
# import individual modules
import my_package.my_module

# must be referenced with its full name
my_package.my_module.my_funtion(my_parameter)

# make it available without its package prefix
from my_package import my_module
my_module.my_function(my_parameter)

# import the desired function or variable directly
from my_package.my_module import my_fuction
my_function(my_parameter)
```
The *import* statement first tests whether the item is defined in the package; if not, it assumes it is a module and attempts to load it. If it fails to find it, an ImportError exeception is raised.  
When using `from package import item*`, the item can be either a submodule (or subpackage) of the package, or some other name defined in the package, like a function, class or variable.  

`from packages import *`  
The import statement uses the following convention: if a package’s "\_\_init\_\_.py" code defines a list named "\_\_all\_\_", it is taken to be the list of module names that should be imported when `from package import *` is encountered.  
For example: if the file "sound/effects/\_\_init__.py" contain the following code:    
`__all__ = ["echo", "surround", "reverse"]`  
This would mean that `from sound.effects import *` would import the three named submodules of the sound package.  

**use *relative imports* based on the name of the current module**  
`from ..filter import equalizer`  

# 7. Input and Output

## 7.1 fancier Output Formatting
1. use *formatted string literals*
```python
# prefix the string with `f` or `F` and write expressions as `{expression}`.
# an optional format specifier can follow the expression 
import math
print(f'The value of pi is approximately {math.pi:.3f}.')
```
2. `str.format()` method
```python
print('We are the {} who say "{}!"'.format('knights', 'Ni'))

# A number in the brackets can be used to refer to the position of the object passed into the str.format() method.
print('{0} and {1}'.format('spam', 'eggs'))

# Keyword argument
print('This {food} is {adjective}.'.format(
      food='spam', adjective='absolutely horrible'))

# pass dict and use '[]' to access the keys, note the number 0 in {} refer to the same first position.
table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 8637678}
print('Jack: {0[Jack]:d}; Sjoerd: {0[Sjoerd]:d}; '
      'Dcab: {0[Dcab]:d}'.format(table))
      
# or
table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 8637678}
print('Jack: {Jack:d}; Sjoerd: {Sjoerd:d}; Dcab: {Dcab:d}'.format(**table))
```
3. do all the string handling yourself  
```python
#add a space between arguments
print(arg1, arg2, end=' ')

# methods of string object
str.rjust()
str.ljust()
str.center()
str.zfill()
```

**a quick display of some varibles**  
`str()` function is meant to return representations of values which are fairly human-readable  
`repr()` is meant to generate representations which can be read by the interpreter.  

## 7.2 Reading and writing files

`open()` returns a file object, and is most commonly used with two arguments: `open(filename, mode)`  
```python
# default open in text mode
f = open('workfile', 'w')

# r: only read (default when mode is omitted)
# w: only write
# a: append
# r+: both read and write

# b: binary mode
```
use the `with` keyword when dealing with file objects. The advantage is that the file is properly closed after its suite finishes, even if an exception is raised at some point.  
```python
with open('workfile') as f:
	read_data = f.read()
	
# now the file has been automatically closed.
```

### 7.2.1 Methods of File Objects
```python
f.read(size)
f.readline()

# read all the lines of a file in a list
list(f)
f.readlines()

f.write('This is a test\n')

# Other types of objects need to be converted – either to a string (in text mode) or a bytes object (in binary mode) – before writing them
value = ('the answer', 42)
s = str(value)  # convert the tuple to string
f.write(s)

# return an integer giving the file's current position.
# represented as number of bytes from the beginning of the file when in binary mode
f.tell()

# change file position in binary mode. In text file, only seeks relative to the beginning of the file are allowed
# add offset to a reference point
# whence (defaults to 0 when omitted)
#	0 begin of file
#	1 current file position
#	2 end of file
f.seek(offset, whence)

f = open('workfile', 'rb+')
f.write(b'0123456789abcdef')

f.seek(5)      # Go to the 6th byte in the file

f.read(1)

f.seek(-3, 2)  # Go to the 3rd byte before the end

f.read(1)
```
### 7.2.2. Saving structured data with json

```python
import json
json.dumps([1, 'simple', 'list'])

# `dump()` serializes to a text file `f`
x = [1, 'simple', 'list']
json.dump(x, f)

# deserialize
x = json.load(f)
```
# 8. Errors and Exceptions

1. *syntax errors*
2. *exceptions* : errors detected during execution

## Handling Exceptions

```python
while True:
    try:
        x = int(input("Please enter a number: "))
        break
    except ValueError:
        print("Oops!  That was no valid number.  Try again...")
    except (RuntimeError, TypeError, NameError):        #An except clause may name multiple exceptions as a parenthesized tuple
        pass   
    except:               # The last except clause may omit the exception name(s)
        pass
    else:
        print('code that must be executed if the try clause does not raise an exception.'
               'Better than adding additional code to the try clause')
        
```

*exception's argument*  
```python
try:
    raise Exception('spam', 'eggs') # 'spam' is excepton's argument
except Exception as inst: #The variable `inst` is bound to an exception instance with the arguments stored in instance.args.
    print(type(inst))    # the exception instance
    print(inst.args)     # arguments stored in .args
    print(inst)          # __str__ allows args to be printed directly,
                         # but may be overridden in exception subclasses
    x, y = inst.args     # unpack args
    print('x =', x)
    print('y =', y)
```

Raising Exceptons  
```python
raise NameError('HiThere')

# re-raise the exception
try:
	raise NameError('HiThere')
except NameError:
	print('An exeception flew by!')
	raise
```

Exception Chaining  
The raise statement allows an optional from which enables chaining exceptions by setting the \_\_cause\_\_ attribute of the raised exception.  
Exception chaining happens automatically when an exception is raised inside an exception handler or finally section.  
Exception chaining can be disabled by using `from None` idiom
```python
def func():
	raise IOEffor
	
try:
	func()
except IOError as exc:
	raise RuntimeError('Failed to open database') from exc
```

User-defined Exceptions  
```python
class Error(Exception):
    """Base class for exceptions in this module."""
    pass

class InputError(Error):
    """Exception raised for errors in the input.

    Attributes:
        expression -- input expression in which the error occurred
        message -- explanation of the error
    """

    def __init__(self, expression, message):
        self.expression = expression
        self.message = message

class TransitionError(Error):
    """Raised when an operation attempts a state transition that's not
    allowed.

    Attributes:
        previous -- state at beginning of transition
        next -- attempted new state
        message -- explanation of why the specific transition is not allowed
    """

    def __init__(self, previous, next, message):
        self.previous = previous
        self.next = next
        self.message = message
```

Defining Clean-up Actions  
```python
try:
    raise KeyboardInterrupt
finally:
    print('Goodbye, world!')
```
	
Predefined Clean-up Actions  
```python
with open("myfile.txt") as f:
    for line in f:
        print(line, end="")
```

# 9. Classes

creating a class creates a new type of object.  
class instance. -- an object
- attribute
- mothod

Module is also an object, and can have attributes. Referencing to module's global names and attribures uses same dot notation.  
`modname.funcname` funcname is an attribute  
`modname.globalName`  

## Python Scopes and Namespaces

Example: the set of built-in names; the global names in a module; and the local names in a function invocation.  
No relation between names in different namespaces.  

Attributes may be read-only or writable.  
```python
modname.the_answer = 42

# delete it
del modname.the_answer
```

Namespaces' lifetime  
1. built-in namespace (live in a module, called `builtins`) is created when the python interpreter starts up, and is never deleted.
2. The global namespace for a module is created when the module definition is read in; normally, modulespaces also last until the interpreter quits.
3. The statements executed by the top-level invocation of the interpreter are part of a module called \_\_main\_\_. They have their own global namespace.
4. The local name for a function is created when the function is called, and deleted when the function returns or raises an exception that is not handled within the function.

A *scope* is a textual region of a Python program where a namespace is directally accessable.  

the actual search for names is done dynamically, at run time. Search sequence:  
1. local name for a function is search first.
2. scopes of enclosing functions. do not search local and global names
3. next-to-last scope contains global names.
4. outermost scope contaning built-in names.

*Scope Test*
1. name declared `global` changes to module's global names.  
2. `nonlocal` changes to inclosing scope. If not declared nonlocal, those variables can be referenced and are read-only 
3. `spam = "local spam"` is local assignment.

```python
def scope_test():
    def do_local():
        spam = "local spam"

    def do_nonlocal():
        nonlocal spam
        spam = "nonlocal spam"

    def do_global():
        global spam
        spam = "global spam"

    spam = "test spam"
    do_local()
    print("After local assignment:", spam)
    do_nonlocal()
    print("After nonlocal assignment:", spam)
    do_global()
    print("After global assignment:", spam)

scope_test()
print("In global scope:", spam)
```
## 9.3. Class

Class definitions, like function definitions (def statements) must be executed before they have any effect.  
The function definitions inside a class normally have a peculiar form of argument list, dictated by the calling conventions for methods.  
When a class definition is entered, a new namespace is created, and used as the local scope.  

### 9.3.2. Class Objects

Class objects support two kinds of operaions:
1. *attribute references* (can be used to change the class later)

```
class MyClass:
    """A simple example class"""
    i = 12345

# the special thing about methods is that the instance object is passed as the first argument of the function.
    def f(self):
        return 'hello world'

MyClass.i = 666
MyClass.__doc__
# "A simple example class"
```
2. *instantiation*

Class instantiation uses function notation. It returns a new instance of the class, called a class object.  
`x = MyClass()`  

```python
class Complex:
    def __init__(self, realpart, imagpart):
        self.r = realpart
        self.i = imagpart

x = Complex(3.0, -4.5)
x.r, x.i
```

### 9.3.3. Instance Objects

Only supports *attribure reference*.  

Two kinds of valid attribure names:
1. data attributes (can be added to instance later)
Data attributes spring into existence when they are first assigned to.  

2. methods
```python
x = MyClass()
x.f         # a method object
MyClass.f   # a function object
```

### 9.3.4. Method Objects

`instance object + function object --> method object`

```python
x.f()

xf = x.f() # method object can be stored away and called at a later time.
xf()
```
### 9.3.5. Class and Instance Variables

*instance variables* are for data unique to each instance.  
*class variables* are for attributes and methods shared by all instances of the class.  

```python
class Dog:

    kind = 'canine'         # class variable shared by all instances

    def __init__(self, name):
        self.name = name    # instance variable unique to each instance
```

```python
class Dog:

    tricks = []             # mistaken use of a class variable

    def __init__(self, name):
        self.name = name

    def add_trick(self, trick):
        self.tricks.append(trick)


class Dog:

    def __init__(self, name):
        self.name = name
        self.tricks = []    # creates a new empty list for each dog

    def add_trick(self, trick):
        self.tricks.append(trick)
```

## 9.4. Random Remarks

If the same attribute name occurs in both an instance and in a class, then attribute lookup prioritizes the instance  
```python
class Warehouse:
    purpose = 'storage'
    region = 'west'
    
w1 = Warehouse()
w1.region = 'east'        # create an instance attribute but not change class attribute
print(Warehouse.region)   # class attribute unchanged.
```
Data may be referenced by methods or ordinary users. Nothing in Python to enforce data hiding.  
Client should use data attributes with care. Clients may add data attributes to an instance object.  

function definition is not necessary enclosed in the class definition: assigning a function object to a local variable in the class is ok.  

Methods may reference global names. The global scope associated with a method is the module.  

Each value is an object, and therefore has a *class* (also called its type). It is stored as object.__class__.  

## 9.5. Inheritance

syntax for derived class:
```python
class DerivedClassName(BaseClassName):
	<statement>
	
class DerivedClassName(modname.BaseClassName):
	<statement>
```
For C++ programmers: all methods in Python are effectively `virtual`.  
Derived classes may override methods of their base classes.  

### 9.5.1. Multiple Inheritance

```python
class DerivedClassName(Base1, Base2, Base3):
    <statement-1>
    .
    .
```
## 9.6. Private Variables

private variables don't exist in Python.  
prefix variables with an underscore `_spam` to indicate "private"  

to avoid name clashes of names defined by subclasses, any identifier of the form `__spam`(two underscores) is replaced with `_classname__spam`  

## 9.8. Iterators

```python
class Reverse:
    """Iterator for looping over a sequence backwards."""
    def __init__(self, data):
        self.data = data
        self.index = len(data)

    def __iter__(self):
        return self

    def __next__(self):
        if self.index == 0:
            raise StopIteration
        self.index = self.index - 1
        return self.data[self.index]

rev = Reverse('spam')
for char in rev:
	print(char)
```

## 9.9. Generators
a simple and powerful tool for creating iterators.  
```python
def reverse(data):
    for index in range(len(data)-1, -1, -1):
        yield data[index]

for char in reverse('golf'):
    print(char)
```

*generator expressions*  
`sum(i*i for i in range(10))`

# 10. Standard Library
```python
import os
os.getcwd()      # Return the current working directory
os.chdir('/server/accesslogs')   # Change current working directory
os.system('mkdir today')   # Run the command mkdir in the system shell

import os
dir(os)
help(os)
```

