# Functions


---

layout: false


## Functions

* Functions are objects that can take some input and return some output.
Functions are the primary way of grouping code into independent units, that can be tested and reused

### Define

* Function definitions start `def`, a name,  parentheses with or without
parameters (comma-separated) and a colon.
* Function parameters are named variables inside the function
* The body of the function is indented with respect to the `def` keyword.
The last line of a function definition is normally a `return` statement and determines the value of a function call


```
>>> def square(x):
...    x2 = x * x
...    return x2

```

---

### Run

* Functions are invoked (executed, run, called) with function name and
  arguments (values) in the parenthesis that match the parameters of the definition. 

```
>>> square(2)
4

```

* Inside the function the parameter `x` becomes a reference to the
  argument `2`. Implicitly there has been an assignment `x = 2`


---

### Optional arguments

* If parameters in a function definition are assigned a default value the
  corresponding argument is optional

~~~
>>> import math
>>> def gaussian(x, x_0=0, a=1):
...     return math.exp(-a*(x - x_0)**2)

>>> gaussian(0.0, a=2.0)
1.0

~~~

* The parameters without and with default values also called positional (required) and keyword (optional).

* Keyword arguments come after positional arguments

---

### Arbitrary arguments

* A function defined to accept any number of positional and keyword arguments. 

~~~
>>> def func(*args, **kwargs):
...     print('args =', args)
...     print('kwargs =', kwargs)
>>> func(1, 2, foo=3, bar=4)
args = (1, 2)
kwargs = {'foo': 3, 'bar': 4}

~~~

* The unnamed arguments (1, 2) form a `tuple`
* The named arguments (foo=3, bar=4) form a `dict`
* The names `args` and `kwargs` are arbitrary 


* A similar syntax can be used when invoking a function
* Setup required arguments in tuple, optional arguments in a dict
* This is a useful feature for passing arguments from function to function
  without requiring an intermediate function to know the details

~~~python
>>> coordinates = (0, )
>>> params = {'x_0': 0, 'a': 1}
>>> gaussian(*coordinates, **params)
1.0

~~~


---
###  doc strings

* A string expression in the beginning of a function body is a doc-string   
* It can be reference with the function attribute `.__doc__`

~~~
>>> def f(x):
...    "Some documentation"
...    ...

~~~

~~~
>>> f.__doc__
'Some documentation'

~~~
* Can be extracted by external tools such as help

~~~
>>> help(f)
Help on function f in module __main__:
<BLANKLINE>
f(x)
    Some documentation
<BLANKLINE>

~~~

---
### `lambda` functions

* Means "make function"
* Used to create short functions on the fly, often functions are expected as
  input argument

~~~
>>> f = lambda x: x**2
>>> f(2)
4

~~~

equivalent to

~~~
>>> def f(x):
...    return x**2

~~~

* Example: sort a list of dictionaries with personal data (name, age) by age
* sorted has an optional argument key: a function of an individual element to
  return a value on which sorting is made

~~~
>>> data = [{'name': 'Alice', 'age': 25}, {'name': 'Bob', 'age': 21}]
>>> for person in sorted(data, key=lambda item: item['age']):
...     print(person['name'], person['age'])
Bob 21
Alice 25

~~~



---
### Variable scope

* Variables inside a function are not valid outside the function (local scope)

~~~
def f(x):
    y = x**2
    return y

print(y) # NameError

~~~

* Variable outside a function are available to the function (global scope)

~~~
>>> def f(x):
...    y = PIH*x**2
...    return y
>>> PIH = math.pi/2
>>> f(1.0)
1.5707963267948966

~~~

---

~~~

## Modules

* a file with Python source
   - name is the filename without the ``.py`` extension
* `import` modules to reuse code
* members of module referenced with dot notation `module.member`

Commonly used Python modules

* ``sys``
* ``os``
* ``math``

---

### The `sys` module

* system modules
* needed e.g. for arguments to a script
* `sys.argv` is a list containing command-line arguments
* The first element `sys.argv [0]` is the file name

~~~
import sys
infile = sys.argv[1]
~~~

### The `os` module

* Interaction with operating system
* Example: execute a unix command 

```
    import os
    os.system('/bin/date')
```

---

### The `math` module

* all basic elementary functions
* fundamental constants

```
    import math
    print(math.sin(math.pi/2))
```


#### Tip

Many use the math modules as a desktop calculator

    $ python
    >>> from math import *
    >>> print(pi/2)
    1.5707963267948966
    >>>

---

### Writing/using your own modules

* Suppose you have written file ``hello.py`` with function ``say_hello``

~~~
#hello.py
def say_hello():
    return "Hello world!"
~~~

* To access the same function in other code, import the module
* Reference the function or variable in the module with dot notation
  `module.member`

~~~
>>> import hello
>>> message = hello.say_hello()
>>> print(message)
Hello world!

~~~

---

