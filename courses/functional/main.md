---
layout: two-cols-header
---

# Functional programming

<br />

<v-click>

- ## Naively: programming with functions

</v-click>

<br />

<v-click>

- ## More precisely: programming with pure functions

</v-click>

<br />

<v-click>

- ## Furthermore: programming with higher-order functions

</v-click>

---
layout: two-cols-header
---

# What is a function?

::left::

<div style="height: 80px;"></div>

::center

![Function](./imgs/function.png){: style="max-width: 200px;" }

::

::right::

Python
```python
def distance(x1, y1, x2, y2):
    return ((x2 - x1) ** 2 + (y2 - y1) ** 2) ** 0.5
```

R
```r
distance <- function(x1, y1, x2, y2) {
  return (sqrt((x2 - x1) ^ 2 + (y2 - y1) ^ 2))
}
```

C++
```cpp
double distance(double x1, double y1, double x2, double y2) {
    return sqrt(pow(x2 - x1, 2) + pow(y2 - y1, 2));
}
```

---
layout: two-cols-header
---

# What is a _pure_ function?

<div style="height: 8px;"></div>

Our `distance` functions are pure, but what makes them so?

::left::

- They are **referentially transparent**:

They always give the same output for the same inputs. You could replace them by their output value in the code without affecting the result.

It doesn’t matter if you replace `sqrt(4)` with `2`, but it does if you replace `today()` with "2025-04-25".

::right::

<v-click>

- They don't have any **side effects**:

The state of the world after they are called is no different than before.

Nothing changes if you call `sqrt(4)` a few times, but `launch_rocket()` is another story.

</v-click>

---
layout: two-cols-header
---

# Impure things

::left::

- Changing the value of a variable
- Modifying a data structure in place
- Printing to the console
- Writing to a file
- Sending data over a network
- Reading from a file or the keyboard
- Fetching data from a database or API
- Getting the current time or date
- Generating a random number

::right::

<v-click>

**These things are necessary.**

So why try to avoid them?

Most useful programs are impure anyway…

</v-click>

---

# Why functional programming?

<div style="height: 8px;"></div>

**Mutability** is the source of countless bugs:

Something somewhere is not what it should be because it got changed by something else.

(“Mutable” is just a fancy word for “can be changed”. “Immutable” means it cannot.)

By limiting the things in your program that can be changed and the parts of it that can change them, bugs become easier to track.

---
layout: two-cols-header
---

# Benefits of functional code

::left::

- **Testability**: pure functions are easily testable as they always produce the same output for a given input.

- **Composability**: pure functions can be combined to create new functions.

- **Parallelizability**: pure functions can be executed in parallel as they don't modify shared state.

::right::

::center

![Functional programming benefits](./imgs/benefits.png){: style="max-width: 300px;" }

::

---
layout: two-cols-header
---

::left::

If you don’t mutate anything ever, you often have to copy lots of data, which can be costly.

Workarounds involve:
- using smart data structures that avoid copying where possible
- using mutability under the hood while providing a functional-style interface

::right::

Pandas data frames are a good example of a smart data structure:

```python
import pandas as pd

data = {'A': [1, 2, 3], 'B': [4, 5, 6]}
df1 = pd.DataFrame(data)
df2 = df1.rename(columns = {'A': 'a'})

print(df2)
```

It offers a functional interface but uses non-functional features under the hood and won’t actually copy data unless it needs to.

---
layout: two-cols
---

The λ-calculus, introduced by Alonzo Church in the 1930s, is the world’s smallest programming language.

It has:
- Variables: `x`, `y`, etc.
- Function definitions: `(λ.xM)`, where `M` is an expression.
- Function applications: `(MN)`, where `M` and `N` are expressions.

Anything that can be computed at all can be computed with this.

::right::

::center

![Alonzo Church](./imgs/Alonzo_Church.jpg){: style="max-width: 300px;" }

::

https://en.wikipedia.org/wiki/File:Alonzo_Church.jpg

---

# Some notable functional lanuages

- Lisp (1960) Heavily inspired by lambda calculus. Second-oldest high-level programming language still in common use. Scheme, Clojure and Logo are dialects. Scheme inspired S which led to R.

- Haskell (1990) The quintessential FP language. Statically typed and “lazy”, with an emphasis on purity. Learn You a Haskell for Great Good! (https://learnyouahaskell.com/) is a great intro to FP.

- Scala (2004) A pragmatic object/functional hybrid language that runs on the Java Virtual Machine.

- F# (2005) Microsoft’s take on FP for the .NET platform. Descended from ML (1973) via Caml (1985) and OCaml (1996).

<v-click>

- **Most** languages also support some measure of functional programming nowadays.

</v-click>

---
layout: two-cols-header
---

::left::

**First-class functions** are functions that can be passed as arguments, returned from functions, or assigned to variables.

**Lambda functions** are small, nameless functions defined in the normal flow of the program.

::right::

```python
# First-class Function
def greet():
    return "Hello"

hello = greet
print(hello())  # Output: Hello

# Lambda function
add = lambda x, y: x + y
print(add(2, 3))  # Output: 5
```

---
layout: two-cols-header
---

::left::

**Higher-order functions** are functions that take other functions as arguments.

**Examples**: `map`, `filter` and `reduce` are built-in higher order functions in Python that use lazy evaluation.

::right::

```python
numbers = [1, 2, 3, 4, 5]

# map
squared= list(map(lambda x: x**2, numbers))
print(squared)
# Output: [1, 4, 9, 16, 25]

# filter
even = list(filter(lambda x: x % 2 == 0, numbers))
print(even)
# Output: [2, 4]

# reduce
from functools import reduce
product= reduce((lambda x, y: x * y), numbers)
print(product)
# Output: 120
```

---
layout: section
---

## Any time you have a collection of things and you need to transform it into another collection of equal length, `map` is what you need.

---

# Map

::center

<div />

![Map function illustration](./imgs/Mapping-steps-loillibe-new.gif){: style="max-width: 650px;" }

::

By <a href="//commons.wikimedia.org/w/index.php?title=User:Loillibe&amp;action=edit&amp;redlink=1" class="new" title="User:Loillibe (page does not exist)">Loillibe</a> - <span class="int-own-work" lang="en">Own work</span>, <a href="https://creativecommons.org/licenses/by-sa/4.0" title="Creative Commons Attribution-Share Alike 4.0">CC BY-SA 4.0</a>, <a href="https://commons.wikimedia.org/w/index.php?curid=73889554">Link</a>

---
layout: two-cols-header
---

# Reductions form trees

::left::

```python
from functools import reduce
reduce((lambda x, y: x + y), [2, 5, 6, 7, 9])
```

<div style="height: 20px;"></div>

::center

![Reduction tree](./imgs/reduction-tree.png){: style="max-width: 350px;" }

::

::right::

Any time you have a collection of things that needs to be boiled down to a single thing, it can be implemented via a reduction.

You already use reduction functions all the time, e.g.: sum, product, mean, stdev, max, min, len, all, any, etc.

---
layout: two-cols-header
---

# Comprehensions and generators in Python

::left::

**Comprehensions** are a more Pythonic way to structure map and filter operations.

**Generators** are similar to list comprehensions but behave differently and aren’t evaluated until iterated over.

::right::

```python
# List comprehension
squared= [x**2 for x in numbers]
print(squared)
# Output: [1, 4, 9, 16, 25]

# Dictionary comprehension
squared_dict= {x: x**2 for x in numbers}
print(squared_dict)
# Output: {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# Generator
squared_gen= (x**2 for x in numbers)
for num in squared_gen:
print(num)
# Output: 1 4 9 16 25
```

---
layout: two-cols-header
---

# Decorators in Python

::left::

Decorators are higher-order functions that take a function as an argument and return another function (that usually enhances or modifies the behavior of the original function).

::right::

```python
def my_decorator(func):
    def wrapper():
        print("Before function call")
        func()
        print("After function call")
    return wrapper

@my_decorator
def say_hello():
    print("Hello")

# > say_hello()
# Before function call
# Hello
# After function call
```

---
layout: three-cols-header
---

# A classic recursion example

<div />

Possible definitions of the factorial function:

::left::

Imperative:

```python
def factorial(n):
    result = 1
    for i in range(2, n + 1):
        result = result * i
    return result
```

::middle::

Mathematical:

$$
n! = \begin{cases} 1 & \text{if } n = 0 \\ n \times (n - 1)! & \text{if } n > 0 \end{cases}
$$

::right::

Functional:

```python
def factorial(n):
    if n == 0:
        return 1
    return n * factorial(n- 1)
```

::bottom::

*Caveats*: What happens if you pass a negative number? Or a really big number?

---
layout: two-cols-header
---

# Conclusions

::left::

Besides benefits like **testability**, **composability** and **parallelizability**, functional programming
changes the way we think about programming.

We shift from an **imperative** mind set (“do this”) to a **declarative** one (“here is what I need”) and
programming becomes about chaining transformations to our data.

A fun little game that captures the experience well:
![https://david-peter.de/cube-composer/](https://david-peter.de/cube-composer/)

::right::

<v-click>

And this is just the tip of the iceberg!

There is a lot more to it than what we have seen today (e.g. monads, currying, pattern matching, algebraic data types, functional reactive programming, ...)

</v-click>

<div style="height: 40px;"></div>
