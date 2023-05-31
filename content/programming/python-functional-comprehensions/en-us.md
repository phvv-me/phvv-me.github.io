---
title: Python list comprehensions and map, filter and reduce
headline: Learning python list comprehensions with map, filter and reduce
date: '2020-08-29'
description: filter, map and reduce are common functional programming patterns that are available in python as builtin functions. However, list comprehensions get us the same results with less lines of code and enhanced readability, making it a necessary pythonic skill.
language: english
category: post
thumbnail:
  src: ../../images/birds-eye-view-photography-beach.jpg
  alt: bird's eye-view photography beach
  author:
    name: Shifaaz Shamoon
    href: https://unsplash.com/@sotti
github: https://github.com/phvv-me/python-functional-comprehensions.git
keywords:
  - python
  - list comprehensions
  - map
  - filter
  - reduce
  - walrus operator
  - functional programming
---

Several languages have a well known set of methods in their arrays and iterators structures. These methods are `filter`, `map`, and `reduce` and they are usually classified as a functional programming pattern.

Python does not implement it as methods, but [has them as builtins](https://docs.python.org/3/library/functions.html) though.Strangely seldom it is we see them being used. Why? Because python offers a much more readable method to perform those operations: list comprehensions.

## What are list comprehensions

### How to `filter()` with list comprehensions

The filter operation does exactly what it says: it filters. This kind of operation is needed when we want a **subset of our list that satisfy some condition**. Some examples would be:

- remove all prime numbers from a set.
- get all even numbers from a list.
- select the strings that start with the letter "a".

Let's see now, how to **build a filter** by implementing the last example. From one step to the other, neither the concept nor the performance shall change, it is all a matter of **productivity and code readability**.

#### the common approach

The filter is implemented as a loop that iterates through all elements of a list and conditionally selects some of them to be part of a new list. It is actually really straightforward and can be implemented as the snippet below.

```python
all_names = ["Arthur", "Pedro", "John", "Aaron", "Paul", "Matthew", "Joseph"]

names_starting_with_a = []
for name in all_names:
    if name.startswith("A"):
        names_starting_with_a.append(name)

assert names_starting_with_a == ["Arthur", "Aaron"]
```

#### isolating the filtering

The filter pattern is considered functional because, in our `if` statement, we are technically calling a _state function_. This is just a function that returns a `bool` based on some logic about the item passed, meaning it _marks the state of the object_. A state function `f` is defined as `f(element) -> bool`, where `element` refers to one element of our list.

For our previous example, we can isolate a `name_startswith_a(name)` state function as seen below.

```python
def name_startswith_a(name):
    return name.startswith("A")

all_names = ["Arthur", "Pedro", "John", "Aaron", "Paul", "Matthew", "Joseph"]

names_starting_with_a = []
for name in all_names:
    if name_startswith_a(name):
        names_starting_with_a.append(name)

assert names_starting_with_a == ["Arthur", "Aaron"]
```

#### with `filter()`

All of that process from before can be simplified with the python `filter()` builtin. From the
[python docs](https://docs.python.org/3/library/functions.html#filter), this function is defined as

```python
def filter(function: Optional[callable], iterable: Iterable) -> Iterator
```

For our example, the first parameter would be our _state function_ and the second our list of names. When adapting it, I noticed that our _state function_ was so straightforward I replaced it for an _anonymous function_. These kinds of functions are [defined in python](https://docs.python.org/3/tutorial/controlflow.html#lambda-expressions) with the `lambda` keyword.

```python
all_names = ["Arthur", "Pedro", "John", "Aaron", "Paul", "Matthew", "Joseph"]

names_starting_with_a_iter = filter(lambda name: name.startswith("A"), all_names)

names_starting_with_a = list(names_starting_with_a_iter)

assert names_starting_with_a == ["Arthur", "Aaron"]
```

There are two things to highlight:

- if `function = None`, `filter()` will use the identity function `lambda x: x` instead
- in order to get a `Sequence` out of `filter`, you must invoke `list()`, `set()` or `tuple()`.

#### with list comprehensions

Python list comprehensions are its way of simplifying the whole process of building a `list` (or any other `Sequence`) while keeping the readability and productivity that python offers. The conversion of `filter()` to a list comprehension can be represented as:

```python
# as filter()
filtered_list = list(filter(state_function, iterable))

# as list comprehension
filtered_list = [element for element in iterable if state_function(element)]
```

For most people, the list comprehension is considered more readable, especially because, in most cases, **a function is not even required**, as we can see in our example below.

```python
all_names = ["Arthur", "Pedro", "John", "Aaron", "Paul", "Matthew", "Joseph"]
names_starting_with_a = [name for name in all_names if name.startswith("A")]

assert names_starting_with_a == ["Arthur", "Aaron"]
```

### How to `map()` with list comprehensions

The map operation is needed when we want to **convert the items of a list**. Some examples would be:

- capitalize all strings in a tuple.
- get the square roots of each number in a set.
- extract the initials from names in a list.

Let's see now, how to **build a map** by implementing the last example. From one step to the other, neither the concept nor the performance shall change, it is all a matter of **productivity and code readability**.

#### the common approach

The map is implemented as a loop that iterates through all elements of a list and appends a changes version of the element into a new list. It is actually really straightforward and can be implemented as the snippet below.

```python
all_names = ["Arthur", "Pedro", "John", "Aaron", "Paul", "Matthew", "Joseph"]

all_initials = []
  for name in all_names:
      initial = name[0] + '.'
      all_initials.append(initial)

assert all_initials == ["A.", "P.", "J.", "A.", "P.", "M.", "J."]
```

#### isolating the mapping

The map pattern is considered functional because, for each element we are technically calling a _mapping function_. This is the function that has the conversion logic. For our previous example, we can isolated a `get_initial_from_name(name)` mapping function as seen below.

```python
all_names = ["Arthur", "Pedro", "John", "Aaron", "Paul", "Matthew", "Joseph"]

def get_initial_from_name(name):
  return name[0] + '.'

all_initials = []
for name in all_names:
    initial = get_initial_from_name(name)
    all_initials.append(initial)

assert all_initials == ["A.", "P.", "J.", "A.", "P.", "M.", "J."]
```

#### with `map()`

All of that process from before can be simplified with the python `map()` builtin. From the
[python docs](https://docs.python.org/3/library/functions.html#map), this function is defined as

```python
def map(function: callable, iterable: Iterable, ...: other_iterables) -> Iterator
```

For our example, the first parameter would be our _mapping function_ and the second our list of names. When adapting it, I noticed that our _mapping function_ was so straightforward I replaced it for an _anonymous function_. These kinds of functions are [defined in python](https://docs.python.org/3/tutorial/controlflow.html#lambda-expressions) with the `lambda` keyword.

```python
all_names = ["Arthur", "Pedro", "John", "Aaron", "Paul", "Matthew", "Joseph"]

all_initials_iter = map(lambda name: name[0] + '.', all_names)

all_initials = list(all_initials_iter)

assert all_initials == ["A.", "P.", "J.", "A.", "P.", "M.", "J."]
```

#### with list comprehensions

The conversion of `map()` to a list comprehension can be represented as:

```python
# as map()
mapped_list = list(map(mapping_function, iterable))

# as list comprehension
mapped_list = [mapping_function(element) for element in iterable]
```

For most people, the list comprehension is considered more readable, especially because, in most cases, **a function is not even required**, as we can see in our example below.

```python
all_names = ["Arthur", "Pedro", "John", "Aaron", "Paul", "Matthew", "Joseph"]

all_initials = [name[0] + '.' for name in all_names]
assert all_initials == ["A.", "P.", "J.", "A.", "P.", "M.", "J."]
```

### How to `reduce()` with list comprehensions

The reduce operation is needed when we want to **aggregate all items of a list**. Some examples would be:

- join all strings in a list into one string.
- concatenate a group of lists into one final list.
- sum a list of numbers.

Let's see now, how to **build a reduce** by implementing the last example.

#### the common approach

The reduce is implemented as a loop that iterates through all elements of a list and **aggregates its elements from an initial value** returning the aggregated value. It is actually really straightforward and can be implemented as the snippet below.

```python
all_ages = [12, 23, 45, 27, 87, 33, 20]

sum_of_ages = 0
for age in all_ages:
    sum_of_ages += age

assert sum_of_ages == sum(all_ages)
```

#### isolating the accumulator

The reduce pattern is considered functional because, for each element we are technically calling an _accumulator function_. This is the function that has the aggregation logic. An accumulator function `f` is defined as `f(accumulated, update) -> new_accumulated`, where `accumulated` is the accumulated value up to that step and `update` refers to one element of our list.

For our previous example, we can isolated an `add_age(total, to_add)` accumulator function as seen below.

```python
all_ages = [12, 23, 45, 27, 87, 33, 20]

def add_age(total, to_add):
    return total + to_add

sum_of_ages = 0
for age in all_ages:
    sum_of_ages = add_age(sum_of_ages, age)

assert sum_of_ages == sum(all_ages)
```

#### with `reduce()`

All of that process from before can be simplified with the python `reduce()` from the standard library via the `functools` module. From the [python docs](https://docs.python.org/3/library/functools.html#functools.reduce), this function is defined as

```python
def reduce(function: Callable[[T, S], T], iterable: Iterable[S], initializer: Optional[T] = None) -> T
```

where `T` is the generic type for the accumulated value and `S` is the generic type for the elements in the iterable.

For our example, the first parameter would be our _accumulator function_, the second our list of ages and the last the initial age. When adapting it, I noticed that our _accumulator function_ was so straightforward I replaced it for the python `add` function available in the `operator` [module from the standard library](https://docs.python.org/3/library/operator.html#operator.add), in which `operator.add(x, y)` is equivalent to the expression `x+y`.

```python
from functools import reduce
from operator import add

all_ages = [12, 23, 45, 27, 87, 33, 20]

initial = 0
sum_of_ages = reduce(add, all_ages, initial)

assert sum_of_ages == sum(all_ages)
```

#### with list comprehensions

The conversion of `reduce()` to a list comprehension is only valid in `python 3.8`, for it requires the [walrus operator](https://docs.python.org/3/whatsnew/3.8.html#assignment-expressions) `:=`, and can be represented as:

```python
from functools import reduce

# as reduce()
result = reduce(accumulator_function, iterable, initial_value)

# as list comprehension
value = 0
accumulated_list = [value := accumulator_function(value, element) for element in iterable]
```

If you noticed, by this way we are not doing exactly what the `functools.reduce()` function proposes, but we are actually doing what `itertools.accumulate()` is meant for! As you can [see from the docs](https://docs.python.org/3/library/itertools.html#itertools.accumulate) and from the snippet above, the `accumulated_list` from obtained with the list comprehensions is roughly equivalent to

```python
from itertools import accumulate

accumulated_list = list(accumulate(accumulator_function, iterable))
```

For most people, the list comprehension is considered more readable, especially because, in most cases, **a function is not even required**, as we can see in our example below.

```python
from itertools import accumulate
from operator import add

all_ages = [12, 23, 45, 27, 87, 33, 20]

sum_of_ages = 0
accumulated_ages = [sum_of_ages := sum_of_ages + age for age in all_ages]  # amazing!

assert sum_of_ages == sum(all_ages)
assert accumulated_ages == list(accumulate(all_ages, add))
```

### map, filter and reduce with python list comprehensions combined

List comprehensions are so powerful we could actually perform the three operations of `filter()`, `map()` and `reduce()` in **a single line of code with python!**

#### pattern

```python
initial_value = 0  # depends on your use case

# equivalent to itertools.accumulate() with map() and filter()
accumulate = [initial_value := accumulator_function(initial_value, mapping_function(element)) for element in sequence if state_function(element)]

# equivalent to functools.reduce()
reduced = accumulate[-1]
```

#### example

For the next example, let's join all the initials from a list of names using only the names with more than 4 letters. Usually we would split this process in 3 steps:

1. filter the list for the names with length over 4
2. map the filtered names to its initials
3. join the result by adding the strings or with `"".join()`

```python
from functools import reduce
from operator import add

awesome_names = ["Amanda", "William", "Bob", "Evangeline", "Mark", "Sarah", "Oliver", "Joe", "Matthew", "Edward"]

# 1. filter
filtered = list(filter(lambda name: len(name) > 4, awesome_names))

# 2. map
mapped = list(map(lambda name: name[0], filtered))

# 3. reduce
reduced = reduce(add, mapped, "")

assert reduced == "".join(mapped)
```

With list comprehensions, however, all of these operations can be performed "simultaneously", meaning that, **for each element, we will invoke the filtering, mapping and reducing process**.

```python
awesome_names = ["Amanda", "William", "Bob", "Evangeline", "Mark", "Sarah", "Oliver", "Joe", "Matthew", "Edward"]

list_comprehension = ""
accumulated = [list_comprehension := list_comprehension + name[0] for name in awesome_names if len(name) > 4]

assert list_comprehension == "AWESOME"
```

> Clean Code Patrol: if you don't actually need the `accumulated` variable but only the joined one, don't use this pattern.

In order to keep your code clear and without _unused variables_, you could replace the python walrus operator `:=` for the `functools.reduce()` method.

```python
from functools import reduce
from operator import add

awesome_names = ["Amanda", "William", "Bob", "Evangeline", "Mark", "Sarah", "Oliver", "Joe", "Matthew", "Edward"]

mapped_and_filtered = [name[0] for name in awesome_names if len(name) > 4]

result = reduce(add, mapped_and_filtered, "")

assert result == "".join(mapped_and_filtered)
```

### What more can we do with list comprehensions?

In the next few sections I'll show you some snippets that apply list comprehensions and can be very useful from time to time.

#### build array with list comprehensions

In this snippet, we build a `5 x 5` identity matrix. The block `1 if x == y else 0` is responsible for selecting the value, and could be seen as the _mapping function_.

```python
matrix = [[1 if x == y else 0 for x in range(5)] for y in range(5)]

assert matrix == [[1, 0, 0, 0, 0],
                  [0, 1, 0, 0, 0],
                  [0, 0, 1, 0, 0],
                  [0, 0, 0, 1, 0],
                  [0, 0, 0, 0, 1]]
```

#### flatten array with list comprehensions

In this snippet, we take a `4 x 4` matrix and _flatten_ it, meaning it becomes a single dimensional array. The code block `for row in matrix for n in row` works just like a nested `for` loop inside the list comprehension.

```python
matrix = [[10, 11, 12, 13],
          [14, 15, 16, 17],
          [18, 19, 20, 21],
          [22, 23, 24, 25]]

flattened = [n for row in matrix for n in row]

assert flattened == list(range(10, 26))
```

#### build dictionary with list comprehensions

It is also possible to construct other types of iterables and sequences with list comprehensions in python. In the next snippet, we build a `dict` from two lists with the python `zip()` [builtin function](https://docs.python.org/3/library/functions.html#zip).

> list comprehension is the name of the programming pattern, so it is not exclusive to lists.

```python
keys = ["a", "b", "c"]
vals = [100, 200, 300]

my_dict = {k: v for k, v in zip(keys, vals)}

assert my_dict == {"a": 100, "b": 200, "c": 300}
```

#### from list of dicts to dict of lists

This is one that each person has their own implementation. I believe that with list comprehensions it becomes simpler and shorter. Besides, many business logics implement this concept with some filters, mappings and fancy names attached to it.

In this snippet, we **group values from the same key in different dicts inside a list in the final dict**.

```python
# list of dicts
lod = [
    {'a': 'hi', 'y': 'bye'},
    {'x': 1, 'y': 2, 'z': 3},
    {'z': 'wow!', 'a': [99, '66']},
]

# flat set of keys
set_of_keys = {key for dic in lod for key in dic.keys()}

# dict of lists
dol = {key: [dic[key] for dic in lod if key in dic] for key in set_of_keys}

assert dol == {
    'a': ['hi', [99, '66']],  # ATTENTION: it does not flatten!
    'x': [1],
    'y': ['bye', 2],
    'z': [3, 'wow!']
}
```

#### from dict of lists to list of dicts

In this snippet, we **flatten the lists building dicts that keep the original order of values**.

> Caveat: if the original dict of lists has None values, these will be ignored by the algorithm below.

```python
from itertools import zip_longest

# dict of lists
dol = {
    'a': ['hi', [99, '66']],
    'x': [1],
    'y': ['bye', 2],
    'z': [3, 'wow!']
}

_keys = dol.keys()
_values = zip_longest(*dol.values())  # this will make all lists "the same size"

lod = [{key: val for key, val in zip(_keys, column) if val is not None} for column in _values]  # then we filter the None values off

assert lod == [
    {'a': 'hi', 'x': 1, 'y': 'bye', 'z': 3},
    {'a': [99, '66'], 'y': 2, 'z': 'wow!'},
]
```

## Conclusions

When I started learning python, the only language I knew by then was C and Fortran, so all iterations I implemented used `for` loops. About an year later, I discovered list comprehensions and struggled a lot to write a simple `map` pattern with it. Personally, I saw no improvement whatsoever.

Indeed, it takes time to adapt to a new pattern, but after it, **you will feel your productivity skyrocketing!** If you are a beginner, take your time and try some other examples as well. I know this might look very odd, but I'm sure it is going to help you when the time comes.

## Further reading

If you are curious about the list comprehension pattern in other programming languages (list comprehension is not a python-exclusive feature), [wikipedia has a good article](https://en.wikipedia.org/wiki/List_comprehension#History) about its theory and history.
