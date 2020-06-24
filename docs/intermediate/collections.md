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
using a `.`. Let\'s dissect it a little more. A named tuple has two
required arguments. They are the tuple name and the tuple field\_names.
In the above example our tuple name was \'Animal\' and the tuple
field\_names were \'name\', \'age\' and \'type\'. Namedtuple makes your
tuples **self-document**. You can easily understand what is going on by
having a quick glance at your code. And as you are not bound to use
integer indexes to access members of a tuple, it makes it more easy to
maintain your code. Moreover, as **\`namedtuple\` instances do not have
per-instance dictionaries**, they are lightweight and require no more
memory than regular tuples. This makes them faster than dictionaries.
However, do remember that as with tuples, **attributes in namedtuples
are immutable**. It means that this would not work:

``` {.python}
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

``` {.python}
from collections import namedtuple

Animal = namedtuple('Animal', 'name age type')
perry = Animal(name="perry", age=31, type="cat")
print(perry[0])
# Output: perry
```

Last but not the least, you can convert a namedtuple to a dictionary.
Like this:

``` {.python}
from collections import namedtuple

Animal = namedtuple('Animal', 'name age type')
perry = Animal(name="Perry", age=31, type="cat")
print(perry._asdict())
# Output: OrderedDict([('name', 'Perry'), ('age', 31), ...
```

