---
title: 3 ways to build a SWITCH in python
headline: 3 ways to refactor if trees with patterns like SWITCH...CASE in python
date: "2020-08-08"
description: how to refactor existing python code if trees into switch patterns using dictionaries, classes and more.
language: english
category: post
outdated: false
thumbnail:
  src: ../../images/mountain-landscape-with-signs-pointing-toward-a-rocky-hiking-path.jpg
  alt: Mountain landscape with signs pointing toward a rocky hiking path
  author:
    name: Jonas Verstuyft
    href: https://unsplash.com/@verstuyftj
github: https://github.com/phvv-me/python-switch-if-tree.git
keywords:
  - python
  - patterns
  - refactoring
  - classes
  - easy-to-refactor
---

<!--
I think this should be shown as details, maybe sidebar

<TooLongDidNotRead title="simple switch pattern">

```python
key = "preposition"
default = "..."

switch = {
    "noun": "dog",
    "verb": "to bark",
    "adjective": "big",
    "adverb": "loudly",
    "preposition": "of",
}.get(key, default)

assert switch == "of"
```

</TooLongDidNotRead>

<TooLongDidNotRead title="nested switch with reduce">

```python
from functools import reduce

switch = {
    "long nested dict": ...
}

path = ("a", "b", "c")
default = "not found"

result = reduce(lambda item, key: item.get(key, default), path, switch)
```

</TooLongDidNotRead>
-->

Python is a language that has many different aspects when compared to other low level languages. It is often that I see C-like syntax in projects that I work on or even in old projects of my own. This is natural as most programmers usually start learning with low level languages and not always specialize on the most particular features that python has to offer.

## The problem at hand

One of the most common subjects of question among python rookies is how to build a _switch...case_ like pattern in python. If you are unaware of what I'm talking about, you can see below how the `SWITCH...CASE` syntax looks like on the C language.

```C
switch(color)
​{
    case "blue":
        printf("The sky is blue");
        break;

    case "yellow":
        printf("The sun is yellow");
        break;

    case "red":
        printf("Blood is red");
        break;

    default:
        printf("I can't thing of anything with that color");

}
```

That is the reason why many people ask if python has a switch case syntax. That is totally understandable, as many low and high level languages have `SWITCH` as a common keyword. However, python has no `SWITCH` or `CASE` statement as you know it. Therefore, very often we come to see the logic of that C snippet as `if...else` trees

```python
if color == "blue":
    print("The sky is blue")
elif color == "yellow":
    print("The sun is yellow")
elif color == "red":
    print("Blood is red")
else:
    print("I can't thing of anything with that color")
```

This might look as harmless for now, but in my experience, code grows. Worse: it tends to grow around the initial pattern they were built with! Thus, we come to see very long `if...else` trees that would look really convoluted in the original `SWITCH...CASE` syntax in C as well.

```python
name = "Thomas Walker"

names = name.split()
if names[0] == "Arthur":
    if names[1] == "Franklin":
        initials = "A.F."
    elif names[1] == "Goodman":
        initials = "A.G."
    elif names[1] == "Walker":
        initials = "A.W."
    else:
        initials = "A."
elif names[0] == "Matthew":
    if names[1] == "Franklin":
        initials = "M.F."
    elif names[1] == "Goodman":
        initials = "M.G."
    elif names[1] == "Walker":
        initials = "M.W."
    else:
        initials = "M."
elif names[0] == "Peter":
    if names[1] == "Franklin":
        initials = "P.F."
    elif names[1] == "Goodman":
        initials = "P.G."
    elif names[1] == "Walker":
        initials = "P.W."
    else:
        initials = "P."
elif names[0] == "Thomas":
    if names[1] == "Franklin":
        initials = "T.F."
    elif names[1] == "Goodman":
        initials = "T.G."
    elif names[1] == "Walker":
        initials = "T.W."
    else:
        initials = "T."
else:
    initials = None
```

The example above might seem useless, but the concept behind it is common while its structure is messy. Instead of getting `initials`, imagine calling a specific function that would send and e-mail customized by family name. Moreover, if this is found on a crucial point in a large codebase, it could definitely **harm the productivity** and be considered **technical debt** for hindering the code comprehension.

## Refactor: `dict`

The structure of the previous snippet recreates the pattern of the `SWITCH` keyword present in other languages: **it compares one value with another set of values until it finds a match or returns the default**. In python, it is fairly simple to refactor the code above into something more readable with `dict`.

```python
switch = {
    'Arthur': {
        'Franklin': 'A.F.',
        'Goodman': 'A.G.',
        'Walker': 'A.W.'
    },
    'Matthew': {
        'Franklin': 'M.F.',
        'Goodman': 'M.G.',
        'Walker': 'M.W.'
    },
    'Peter': {
        'Franklin': 'P.F.',
        'Goodman': 'P.G.',
        'Walker': 'P.W.'
    },
    'Thomas': {
        'Franklin': 'T.F.',
        'Goodman': 'T.G.',
        'Walker': 'T.W.'
    },
}

names = "Thomas Walker".split()
initials = switch.get(names[0]).get(names[1], f"{names[0]}.")
```

As shown above, the simplest way to build the _switch pattern_ in python is with the `.get(key, default=None)` method in the `dict` data structure. It can perform exactly what `SWITCH...CASE` proposes, but in a much more readable fashion than `if...else` trees.

I am not saying, however, that all `if...else` statements could nor should be refactored into dictionaries. What I am doing is showing a pattern that is much easier to read and to edit that the previous one. We still have to consider the logic behind it.

This pattern can be very useful for function selection as well. Since functions are first-class citizens in python, we could build a library with several different implementations for a single concept. The example below presents the idea on how to do it with different fibonacci implementations:

```python
def fibonacci_switch(key):
    def loop(n):
        ...

    def recurrent(n):
        ...

    def memoization(n):
        ...

    # you could refactor this as a loop
    return {
        loop.__name__: loop,
        recurrent.__name__: recurrent,
        memoization.__name__: memoization,
    }.get(key, lambda: NotImplemented)


memoization_fibonacci = fibonacci_switch("memoization")

assert fibonacci(10) == 55
```

## Refactor: `dict` + `reduce`

I find very common to hear that this pattern, however is too limited, especially when you have _nested if trees_. Since `dict` can receive any type, even if we have a long nested tree, we might be able to refactor it as a `dict`. Take, for instance, the crazy switch below.

```python
switch = {
    "noun": {
        "animal": {
          "mammal": "rabbit",
          "reptile": "tortoise"
        },
        "human": "Napoleon Bonaparte",
    },
    "verb": {
        "witchcraft": {
          "summon",
          "enchant",
          "dispel"
        },
        "sports": {
            "basketball": 5,
            "soccer": 11,
            "volleyball": 7,
            "sumo": 2,
            "darts": 1,
        },
    },
    "adjective": {
        "good": {
          "excellent": 10,
          "very good": 8,
          "okay": 6,
        },
        "bad": {
          "unbearable": 0,
          "terrible": 2,
          "awful": 4,
        },
    },
    "adverb": ...,
}
```

For nested switches, what we want to define is a `path`: it simply represents the _sequence of keys_ for accessing each level. In our example, let's make

```python
path = ("verb", "sports", "sumo")
default = "not found"
```

Now, the most direct to reach our value would be to perform a loop as the one below. We can even add a `try...except` block to leave as soon as we don't receive a `dict` (as only `dict` has `.get()` method **in our switch**).

```python
item = switch
for key in path:
    try:
        item = item.get(key, default)
    except AttributeError:
        break
```

This is fair, I tell you, but let me show now an even simpler way to make the previous switch pattern even more readable.

```python
from functools import reduce

result = reduce(lambda item, key: item.get(key, default), path, switch)
```

With the `reduce` function available in the python standard library, we can make the previous `for` loop an _one-liner_. It is true I'm cheating here, for there is no `dict` checking with `try..catch`, but it still works because the `path` in this example is a valid one. You can refactor the anonymous `lambda` function into a _proper_ function though.

## Refactor: `__init_subclass__`

The final `SWITCH...CASE` refactor I want to show in python might come off as _too much_, but it is the one I believe to be the most elegant of all. Besides, I actually used it in a real world project! Therefore, I think it is important to present it here.

```python
if fruit.kind == "apple":
    result = actions.juice(fruit)
elif fruit.kind == "orange":
    result = actions.cut(fruit)
elif fruit.kind == "banana":
    result = actions.peel(fruit)
else:
    raise ValueError(f"{fruit.kind} is not available")

energy = actions.eat(result)

if fruit.kind == "apple":
    result = evaluate(energy, fruit)
elif fruit.kind == "orange":
    result = evaluate(fruit=fruit)
elif fruit.kind == "banana":
    result = evaluate(energy)
else:
    raise ValueError(f"{fruit.kind} is not available")

process(result)
```

The `if...else` tree above might seem very straightforward and maybe you find it unnecessary to refactor it at all. I argue however that **you ought not see the code by what it is, but by what it can become.** As a matter of fact, the idea of replicating this `if...else` pattern will difficult the work of future contributors.

I believe that, with experience, a good developer would be able to see this pattern before it causes too much trouble and refactor it in a way it doesn't hinder future productivity. For this example, we will refactor it as a _class-based dispatcher_ with the `dict` _switch pattern_. Besides, everything will be fairly simplified thanks to the awesome `__init_subclass__` dunder method.

```python
class BaseFruitModel():
    registry = {}

    def __init_subclass__(cls, fruit):
        # register the child class as subclassed
        BaseFruitModel.registry[fruit] = cls
```

The [dunder init subclass magic method](https://python.readthedocs.io/fr/stable/reference/datamodel.html#object.__init_subclass__) is _called whenever the containing class is subclassed_. `cls` _is then the new subclass_. This allows us to _register_ other classes in a single reference "dynamically": We just need to subclass `BaseFruitModel` and it will become a new branch in our _switch_.

```python
class AppleModel(BaseFruitModel, fruit="apple"):
    def make_juice(self):
      ...
      return "apple juice"

class OrangeModel(BaseFruitModel, fruit="orange"):
    def cut(self):
        ...
        return "cut orange"

class BananaModel(BaseFruitModel, fruit="banana"):
    def peel(self):
        ...
        return "peeled 12 bananas"
```

Now, whenever I want to add a new fruit, I just need to come to the bottom of this file and add my new _Fruit_ class subclassing `BaseFruitModel` and setting a fruit. It is even possible to automate the the `registry` key definition by using the class name as key with `cls.__name__` if you want to.

```python
class BaseRegistry():
    registry = {}

    def __init_subclass__(cls):
        BaseFruitModel.registry[cls.__name__] = cls
```

Now, we still need to do a little more to actually be able to make the whole process functional. First, we add an _Abstract Base Class_ to define our `BaseFruitModel` as an interface. Then we can add some `abstractmethods` and even a _global method_ that calls the common interface in our registered models.

```python
from abc import ABC, abstractmethod

class BaseFruitModel(ABC):
    registry = {}

    def __init_subclass__(cls, fruit):
        # register the child class as subclassed
        BaseFruitModel.registry[fruit] = cls

    @abstractmethod
    def prepare(self, fruit):
        raise NotImplementedError

    @abstractmethod
    def evaluate(self, energy=None, fruit=None):
        raise NotImplementedError

    def eat(self, fruit):
        fruits = self.registry.get(fruit).prepare(fruit)
        return f"you did: {fruits}. Delicious!"
```

However, we have a lot of methods that share the same arguments. This is looks like it could be part of `self`. Since `fruit` is the only thing we need to initialize our classes, we can use `dataclasses` to define the `__init__` method automatically. a `dataclass` requires we set a type for `fruit`, I will use `Mapping` here, but you could use `Any` or a custom `Fruit` class if it makes sense.

```python
from dataclasses import dataclass
from typing import Hashable, Mapping, Optional

@dataclass
class BaseFruitModel(ABC):
    fruit: Mapping
    energy: Optional[str] = None

    registry = {}

    def __init_subclass__(cls, /, fruit: Hashable, **kwargs):
        super().__init_subclass__(**kwargs)
        # register the child class as subclassed
        BaseFruitModel.registry[fruit] = cls

    @abstractmethod
    def prepare(self):
        raise NotImplementedError

    @abstractmethod
    def evaluate(self):
        raise NotImplementedError

    def eat(self):
        fruits = self.registry.get(self.fruit).prepare()
        return f"you did: {fruits}. Delicious!"
```

For most cases, this approach might seem overkill, I know, but some time ago I had to use a pattern just like this while developing a function that would select a _neural network model_ based on input data. As I was using class-based models in `tensorflow` already, this `BaseRegistry` class came as a _mixin_ to each of my custom models. Then, it became much easier to perform the _model selection_.

## Conclusions

`if...else` trees are one of the most common code smells I find in python code. It is so simple to start an `if` statement to select something that is also very common to keep it there forever.

On the other hand, python offers patterns better than the traditional switch case syntax in an easy-to-refactor style. Therefore, if you've seen convoluted `if...else` trees in some code you're working on, this is your chance to refactor it.

I hope you enjoyed this post and, as always, Happy Coding 🧑🏻‍💻