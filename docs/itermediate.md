[TOC]



# Collections

Python ships with a module that contains a number of container data
types called Collections:

-   `Counter`
-   `namedtuple`


## Counter


Counter allows us to count the occurrences of a particular item. For
instance it can be used to count the number of individual favourite
colours:

``` python
from collections import Counter

colours = (
    ('Jack', 'Yellow'),
    ('Bob', 'Blue'),
    ('Alice', 'Green'),
    ('Simon', 'Black'),
    ('Bob', 'Red'),
    ('Alice', 'Silver'),
)

favs = Counter(name for name, colour in colours)
print(favs)
```

We can also count the most common lines in a file using it. For example:

``` python
with open('filename', 'rb') as f:
    line_count = Counter(f)
print(line_count)
```

## namedtuple


You might already be acquainted with tuples. A tuple is basically a
immutable list which allows you to store a sequence of values separated
by commas. They are just like lists but have a few key differences. The
major one is that unlike lists, **you can not reassign an item in a
tuple**. In order to access the value in a tuple you use integer indexes
like:

``` python
man = ('Ali', 30)
print(man[0])
# Output: Ali
```

Well, so now what are `namedtuples`? They turn tuples into convenient
containers for simple tasks. With namedtuples you don\'t have to use
integer indexes for accessing members of a tuple. You can think of
namedtuples like dictionaries but unlike dictionaries they are
immutable.

``` python
from collections import namedtuple

Animal = namedtuple('Animal', 'name age type')
perry = Animal(name="perry", age=31, type="cat")

print(perry)
# Output: Animal(name='perry', age=31, type='cat')

print(perry.name)
# Output: 'perry'
```

You can now see that we can access members of a tuple just by their name
using a `.`. Let's dissect it a little more. A named tuple has two
required arguments. They are the tuple name and the tuple field\_names.
In the above example our tuple name was 'Animal' and the tuple
field_names were 'name', 'age' and 'type'. Namedtuple makes your
tuples **self-document**. You can easily understand what is going on by
having a quick glance at your code. And as you are not bound to use
integer indexes to access members of a tuple, it makes it more easy to
maintain your code. Moreover, as **`namedtuple` instances do not have
per-instance dictionaries**, they are lightweight and require no more
memory than regular tuples. This makes them faster than dictionaries.
However, do remember that as with tuples, **attributes in namedtuples
are immutable**. It means that this would not work:

``` python
from collections import namedtuple

Animal = namedtuple('Animal', 'name age type')
perry = Animal(name="perry", age=31, type="cat")
perry.age = 42

# Output: Traceback (most recent call last):
#            File "", line 1, in
#         AttributeError: can't set attribute
```

You should use named tuples to make your code self-documenting. **They
are backwards compatible with normal tuples**. It means that you can use
integer indexes with namedtuples as well:

``` python
from collections import namedtuple

Animal = namedtuple('Animal', 'name age type')
perry = Animal(name="perry", age=31, type="cat")
print(perry[0])
# Output: perry
```

Last but not the least, you can convert a namedtuple to a dictionary.
Like this:

``` python
from collections import namedtuple

Animal = namedtuple('Animal', 'name age type')
perry = Animal(name="Perry", age=31, type="cat")
print(perry._asdict())
# Output: OrderedDict([('name', 'Perry'), ('age', 31), ...
```



# Comprehensions


Comprehensions are constructs that allow
sequences to be built from other sequences. Several types of
comprehensions are supported:

* list comprehensions
* dictionary comprehensions
* set comprehensions
* generator comprehensions

## `list` comprehensions

List comprehensions provide a short and concise way to create lists. It
consists of square brackets containing an expression followed by a `for`
clause, then zero or more `for` or `if` clauses. The expressions can be
anything, meaning you can put in all kinds of objects in lists. The
result would be a new list made after the evaluation of the expression
in context of the `if` and `for` clauses.

**Blueprint**

``` python
variable = [out_exp for out_exp in input_list if out_exp == 2]
```

Here is a short example:

``` python
multiples = [i for i in range(30) if i % 3 == 0]
print(multiples)
# Output: [0, 3, 6, 9, 12, 15, 18, 21, 24, 27]
```

This can be really useful to make lists quickly. It is even preferred by
some instead of the `filter` function. List comprehensions really shine
when you want to supply a list to a method or function to make a new
list by appending to it in each iteration of the `for` loop. For
instance you would usually do something like this:

``` python
squared = []
for x in range(10):
    squared.append(x**2)
```

You can simplify it using list comprehensions. For example:

``` python
squared = [x**2 for x in range(10)]
```

## `dict` comprehensions


They are used in a similar way. Here is an example which I found
recently:

``` python
mcase = {'a': 10, 'b': 34, 'A': 7, 'Z': 3}

mcase_frequency = {
    k.lower(): mcase.get(k.lower(), 0) + mcase.get(k.upper(), 0)
    for k in mcase.keys()
}

# mcase_frequency == {'a': 17, 'z': 3, 'b': 34}
```

In the above example we are combining the values of keys which are same
but in different typecase. I personally do not use `dict` comprehensions
a lot. You can also quickly switch keys and values of a dictionary:

``` {.python}
{v: k for k, v in some_dict.items()}
```

## `set` comprehensions

They are also similar to list comprehensions. The only difference is
that they use braces `{}`. Here is an example:

``` .python
squared = {x**2 for x in [1, 1, 2]}
print(squared)
# Output: {1, 4}
```

## `generator` comprehensions


They are also similar to list comprehensions. The only difference is
that they don't allocate memory for the whole list but generate one
item at a time, thus more memory efficient.

``` python
multiples_gen = (i for i in range(30) if i % 3 == 0)
print(multiples_gen)
# Output: <generator object <genexpr> at 0x7fdaa8e407d8>
for x in multiples_gen:
  print(x)
  # Outputs numbers
```

# Decorators

Decorators dynamically alter the functionality of a function, method, 
or class without having to directly use subclasses or change the source code of 
the function being decorated.


## Defining functions within functions:

In Python we can define functions inside other functions:

``` python
def hi(name="bigriver"):
    print("now you are inside the hi() function")

    def greet():
        return "now you are in the greet() function"

    def welcome():
        return "now you are in the welcome() function"

    print(greet())
    print(welcome())
    print("now you are back in the hi() function")

hi()
#output:now you are inside the hi() function
#       now you are in the greet() function
#       now you are in the welcome() function
#       now you are back in the hi() function

# This shows that whenever you call hi(), greet() and welcome()
# are also called. However the greet() and welcome() functions
# are not available outside the hi() function e.g:

greet()
#outputs: NameError: name 'greet' is not defined
```

So now we know that we can define functions in other functions. In other
words: we can make nested functions. Now you need to learn one more
thing, that functions can return functions too.

## Returning functions from within functions:


It is not necessary to execute a function within another function, we
can return it as an output as well:

``` python
def hi(name="bigriver"):
    def greet():
        return "now you are in the greet() function"

    def welcome():
        return "now you are in the welcome() function"

    if name == "bigriver":
        return greet
    else:
        return welcome

a = hi()
print(a)
#outputs: <function greet at 0x7f2143c01500>

#This clearly shows that `a` now points to the greet() function in hi()
#Now try this

print(a())
#outputs: now you are in the greet() function
```

Just take a look at the code again. In the `if else` clause we are
returning `greet` and `welcome`, not `greet()` and `welcome()`. Why is
that? It's because when you put a **pair of parentheses** after it, the
function gets executed; whereas if you don't put parenthesis after it,
then it can be passed around and can be assigned to other variables
without executing it. Did you get it? Let me explain it in a little bit
more detail. When we write `a = hi()`, `hi()` gets executed and because
the name is bigriver by default, the function `greet` is returned. If we
change the statement to `a = hi(name = "ali")` then the `welcome`
function will be returned. We can also do print `hi()()` which outputs
*now you are in the greet() function*.

## Giving a function as an argument to another function:


``` python
def hi():
    return "hi bigriver!"

def doSomethingBeforeHi(func):
    print("I am doing some boring work before executing hi()")
    print(func())

doSomethingBeforeHi(hi)
#outputs:I am doing some boring work before executing hi()
#        hi bigriver!
```

Now you have all the required knowledge to learn what decorators really
are. Decorators let you execute code before and after a function.

## Writing your first decorator:


In the last example we actually made a decorator! Let\'s modify the
previous decorator and make a little bit more usable program:

``` python
def a_new_decorator(a_func):

    def wrapTheFunction():
        print("I am doing some boring work before executing a_func()")

        a_func()

        print("I am doing some boring work after executing a_func()")

    return wrapTheFunction

def a_function_requiring_decoration():
    print("I am the function which needs some decoration to remove my foul smell")

a_function_requiring_decoration()
#outputs: "I am the function which needs some decoration to remove my foul smell"

a_function_requiring_decoration = a_new_decorator(a_function_requiring_decoration)
#now a_function_requiring_decoration is wrapped by wrapTheFunction()

a_function_requiring_decoration()
#outputs:I am doing some boring work before executing a_func()
#        I am the function which needs some decoration to remove my foul smell
#        I am doing some boring work after executing a_func()
```

Did you get it? We just applied the previously learned principles. This
is exactly what the decorators do in Python! They wrap a function and
modify its behaviour in one way or another. Now you might be wondering
why we did not use the @ anywhere in our code? That is just a short way
of making up a decorated function. Here is how we could have run the
previous code sample using @.

``` python
@a_new_decorator
def a_function_requiring_decoration():
    """Hey you! Decorate me!"""
    print("I am the function which needs some decoration to "
          "remove my foul smell")

a_function_requiring_decoration()
#outputs: I am doing some boring work before executing a_func()
#         I am the function which needs some decoration to remove my foul smell
#         I am doing some boring work after executing a_func()

#the @a_new_decorator is just a short way of saying:
a_function_requiring_decoration = a_new_decorator(a_function_requiring_decoration)
```

I hope you now have a basic understanding of how decorators work in
Python. Now there is one problem with our code. If we run:

``` python
print(a_function_requiring_decoration.__name__)
# Output: wrapTheFunction
```

That's not what we expected! Its name is
"a_function_requiring_decoration". Well, our function was replaced
by wrapTheFunction. It overrode the name and docstring of our function.
Luckily, Python provides us a simple function to solve this problem and
that is `functools.wraps`. Let's modify our previous example to use
`functools.wraps`:

``` python
from functools import wraps

def a_new_decorator(a_func):
    @wraps(a_func)
    def wrapTheFunction():
        print("I am doing some boring work before executing a_func()")
        a_func()
        print("I am doing some boring work after executing a_func()")
    return wrapTheFunction

@a_new_decorator
def a_function_requiring_decoration():
    """Hey yo! Decorate me!"""
    print("I am the function which needs some decoration to "
          "remove my foul smell")

print(a_function_requiring_decoration.__name__)
# Output: a_function_requiring_decoration
```

Now that is much better. Let\'s move on and learn some use-cases of
decorators.

**Blueprint:**

``` python
from functools import wraps
def decorator_name(f):
    @wraps(f)
    def decorated(*args, **kwargs):
        if not can_run:
            return "Function will not run"
        return f(*args, **kwargs)
    return decorated

@decorator_name
def func():
    return("Function is running")

can_run = True
print(func())
# Output: Function is running

can_run = False
print(func())
# Output: Function will not run
```

Note: `@wraps` takes a function to be decorated and adds the
functionality of copying over the function name, docstring, arguments
list, etc. This allows us to access the pre-decorated function\'s
properties in the decorator.

### Use-cases:

Now let\'s take a look at the areas where decorators really shine and
their usage makes something really easy to manage.

Authorization \~\~\~\~\~\~\~\~\~\~\~\~

Decorators can help to check whether someone is authorized to use an
endpoint in a web application. They are extensively used in Flask web
framework and Django. Here is an example to employ decorator based
authentication:

**Example :**

``` {.python}
from functools import wraps

def requires_auth(f):
    @wraps(f)
    def decorated(*args, **kwargs):
        auth = request.authorization
        if not auth or not check_auth(auth.username, auth.password):
            authenticate()
        return f(*args, **kwargs)
    return decorated
```

### Logging


Logging is another area where the decorators shine. Here is an example:

``` {.python}
from functools import wraps

def logit(func):
    @wraps(func)
    def with_logging(*args, **kwargs):
        print(func.__name__ + " was called")
        return func(*args, **kwargs)
    return with_logging

@logit
def addition_func(x):
   """Do some math."""
   return x + x


result = addition_func(4)
# Output: addition_func was called
```

I am sure you are already thinking about some clever uses of decorators.

## Decorators with Arguments


Come to think of it, isn't `@wraps` also a decorator? But, it takes an
argument like any normal function can do. So, why can\'t we do that too?

This is because when you use the `@my_decorator` syntax, you are
applying a wrapper function with a single function as a parameter.
Remember, everything in Python is an object, and this includes
functions! With that in mind, we can write a function that returns a
wrapper function.

### Nesting a Decorator Within a Function


Let's go back to our logging example, and create a wrapper which lets
us specify a logfile to output to.

``` python
from functools import wraps

def logit(logfile='out.log'):
    def logging_decorator(func):
        @wraps(func)
        def wrapped_function(*args, **kwargs):
            log_string = func.__name__ + " was called"
            print(log_string)
            # Open the logfile and append
            with open(logfile, 'a') as opened_file:
                # Now we log to the specified logfile
                opened_file.write(log_string + '\n')
            return func(*args, **kwargs)
        return wrapped_function
    return logging_decorator

@logit()
def myfunc1():
    pass

myfunc1()
# Output: myfunc1 was called
# A file called out.log now exists, with the above string

@logit(logfile='func2.log')
def myfunc2():
    pass

myfunc2()
# Output: myfunc2 was called
# A file called func2.log now exists, with the above string
```

### Decorator Classes


Now we have our logit decorator in production, but when some parts of
our application are considered critical, failure might be something that
needs more immediate attention. Let\'s say sometimes you want to just
log to a file. Other times you want an email sent, so the problem is
brought to your attention, and still keep a log for your own records.
This is a case for using inheritence, but so far we\'ve only seen
functions being used to build decorators.

Luckily, classes can also be used to build decorators. So, let\'s
rebuild logit as a class instead of a function.

``` python
class logit(object):

       _logfile = 'out.log'
   
    def __init__(self, func):
        self.func = func

       def __call__(self, *args):
           log_string = self.func.__name__ + " was called"
        print(log_string)
        # Open the logfile and append
           with open(self._logfile, 'a') as opened_file:
            # Now we log to the specified logfile
            opened_file.write(log_string + '\n')
        # Now, send a notification
        self.notify()

           # return base func
           return self.func(*args)

           

    def notify(self):
        # logit only logs, no more
        pass
```

This implementation has an additional advantage of being much cleaner
than the nested function approach, and wrapping a function still will
use the same syntax as before:

``` python
   logit._logfile = 'out2.log' # if change log file
   @logit
   def myfunc1():
       pass

   myfunc1()
   # Output: myfunc1 was called
```

Now, let's subclass logit to add email functionality (though this topic
will not be covered here).

``` python
class email_logit(logit):
    '''
    A logit implementation for sending emails to admins
    when the function is called.
    '''
    def __init__(self, email='admin@myproject.com', *args, **kwargs):
        self.email = email
        super(email_logit, self).__init__(*args, **kwargs)

    def notify(self):
        # Send an email to self.email
        # Will not be implemented here
        pass
```

From here, `@email_logit` works just like `@logit` but sends an email to
the admin in addition to logging.

# Enumerate


Enumerate is a built-in function of Python. Its usefulness can not be
summarized in a single line. Yet most of the newcomers and even some
advanced programmers are unaware of it. It allows us to loop over
something and have an automatic counter. Here is an example:

``` {.python}
for counter, value in enumerate(some_list):
    print(counter, value)
```

And there is more! `enumerate` also accepts an optional argument which
makes it even more useful.

``` {.python}
my_list = ['apple', 'banana', 'grapes', 'pear']
for c, value in enumerate(my_list, 1):
    print(c, value)

# Output:
# 1 apple
# 2 banana
# 3 grapes
# 4 pear
```

The optional argument allows us to tell `enumerate` from where to start
the index. You can also create tuples containing the index and list item
using a list. Here is an example:

``` {.python}
my_list = ['apple', 'banana', 'grapes', 'pear']
counter_list = list(enumerate(my_list, 1))
print(counter_list)
# Output: [(1, 'apple'), (2, 'banana'), (3, 'grapes'), (4, 'pear')]
```

# File Handling


## Ignore Rows

skip header row

``` python
with open(fname) as f:
    next(f)
    for line in f:
        #do something
```

ignore blank lines

``` python
def nonblank_lines(f):
    for l in f:
        line = l.rstrip()
        if line:
            yield line

with open(filename) as f_in:
    for line in nonblank_lines(f_in):
        # Stuff
```



# Generators


First lets understand iterators. According to Wikipedia, an iterator is
an object that enables a programmer to traverse a container,
particularly lists. However, an iterator performs traversal and gives
access to data elements in a container, but does not perform iteration.
You might be confused so lets take it a bit slow. There are three parts
namely:

-   Iterable
-   Iterator
-   Iteration

All of these parts are linked to each other. We will discuss them one by
one and later talk about generators.

## Iterable


An `iterable` is any object in Python which has an `__iter__` or a
`__getitem__` method defined which returns an **iterator** or can take
indexes (You can read more about them
[here](https://stackoverflow.com/a/20551346)). In short an `iterable` is
any object which can provide us with an **iterator**. So what is an
**iterator**?

## Iterator


An iterator is any object in Python which has a `next` (Python2) or
`__next__` method defined. That\'s it. That\'s an iterator. Now let\'s
understand **iteration**.

## Iteration


In simple words it is the process of taking an item from something e.g a
list. When we use a loop to loop over something it is called iteration.
It is the name given to the process itself. Now as we have a basic
understanding of these terms let\'s understand **generators**.

## Generators {#generators-1}


Generators are iterators, but you can only iterate over them once. It's
because they do not store all the values in memory, they generate the
values on the fly. You use them by iterating over them, either with a
\'for\' loop or by passing them to any function or construct that
iterates. Most of the time `generators` are implemented as functions.
However, they do not `return` a value, they `yield` it. Here is a simple
example of a `generator` function:

``` {.python}
def generator_function():
    for i in range(10):
        yield i

for item in generator_function():
    print(item)

# Output: 0
# 1
# 2
# 3
# 4
# 5
# 6
# 7
# 8
# 9
```

It is not really useful in this case. Generators are best for
calculating large sets of results (particularly calculations involving
loops themselves) where you don\'t want to allocate the memory for all
results at the same time. Many Standard Library functions that return
`lists` in Python 2 have been modified to return `generators` in Python
3 because `generators` require fewer resources.

Here is an example `generator` which calculates fibonacci numbers:

``` {.python}
# generator version
def fibon(n):
    a = b = 1
    for i in range(n):
        yield a
        a, b = b, a + b
```

Now we can use it like this:

``` {.python}
for x in fibon(1000000):
    print(x)
```

This way we would not have to worry about it using a lot of resources.
However, if we would have implemented it like this:

``` {.python}
def fibon(n):
    a = b = 1
    result = []
    for i in range(n):
        result.append(a)
        a, b = b, a + b
    return result
```

It would have used up all our resources while calculating a large input.
We have discussed that we can iterate over `generators` only once but we
haven\'t tested it. Before testing it you need to know about one more
built-in function of Python, `next()`. It allows us to access the next
element of a sequence. So let\'s test out our understanding:

``` {.python}
def generator_function():
    for i in range(3):
        yield i

gen = generator_function()
print(next(gen))
# Output: 0
print(next(gen))
# Output: 1
print(next(gen))
# Output: 2
print(next(gen))
# Output: Traceback (most recent call last):
#            File "<stdin>", line 1, in <module>
#         StopIteration
```

As we can see that after yielding all the values `next()` caused a
`StopIteration` error. Basically this error informs us that all the
values have been yielded. You might be wondering why we don\'t get this
error when using a `for` loop? Well the answer is simple. The `for` loop
automatically catches this error and stops calling `next`. Did you know
that a few built-in data types in Python also support iteration? Let\'s
check it out:

``` {.python}
my_string = "Yasoob"
next(my_string)
# Output: Traceback (most recent call last):
#      File "<stdin>", line 1, in <module>
#    TypeError: str object is not an iterator
```

Well that\'s not what we expected. The error says that `str` is not an
iterator. Well it\'s right! It\'s an iterable but not an iterator. This
means that it supports iteration but we can\'t iterate over it directly.
So how would we iterate over it? It\'s time to learn about one more
built-in function, `iter`. It returns an `iterator` object from an
iterable. While an `int` isn\'t an iterable, we can use it on string!

``` {.python}
int_var = 1779
iter(int_var)
# Output: Traceback (most recent call last):
#   File "<stdin>", line 1, in <module>
# TypeError: 'int' object is not iterable
# This is because int is not iterable

my_string = "Yasoob"
my_iter = iter(my_string)
print(next(my_iter))
# Output: 'Y'
```

Now that is much better. I am sure that you loved learning about
generators. Do bear it in mind that you can fully grasp this concept
only when you use it. Make sure that you follow this pattern and use
`generators` whenever they make sense to you. You won\'t be
disappointed!

# Lambdas

Lambdas are one line functions. They are also known as anonymous
functions in some other languages.

**Blueprint**

``` python
lambda argument: manipulate(argument)
```

**Example**

``` python
add = lambda x, y: x + y

print(add(3, 5))
# Output: 8
```

Here are a few useful use cases for lambdas and just a few ways in which
they are used in the wild:

**List sorting**

``` python
a = [(1, 2), (4, 1), (9, 10), (13, -3)]
a.sort(key=lambda x: x[1])

print(a)
# Output: [(13, -3), (4, 1), (1, 2), (9, 10)]
```

**Parallel sorting of lists**

``` python
data = zip(list1, list2)
data = sorted(data)
list1, list2 = map(lambda t: list(t), zip(*data))
```




class A(object):
    def foo(self, x):
        print "executing foo(%s, %s)" % (self, x)

    @classmethod
    def class_foo(cls, x):
        print "executing class_foo(%s, %s)" % (cls, x)
    
    @staticmethod
    def static_foo(x):
        print "executing static_foo(%s)" % x    

a = A()
# Typing

[`typing`](https://docs.python.org/3/library/typing.html#module-typing) : Support for type hints.

```
def greeting(name: str) -> str:
return 'Hello ' + name
```

In the function `greeting`, the argument `name` is expected to be of type `str` and the return type `str` Subtypes are accepted as arguments

[`typing.Union`](https://docs.python.org/3/library/typing.html#typing.Union)

`Union[X,  Y]`  means either X or Y


