---
layout: single
title:  "Python: List"
date:   2021-12-16 15:02:15 +0500
categories: python
tag: python
toc: true
toc_label: "On This Post"
toc_sticky: true
---

## Lists
Python knows a number of compound data types, used to group together other values. The most versatile is the list, which can be written as a list of comma-separated values (items) between square brackets. Lists might contain items of different types, but usually the items all have the same type.

```py
In [1]: squares = [1, 4, 9, 16, 25]                            

In [2]: print(squares)                                         
[1, 4, 9, 16, 25]
```

Like strings (and all other built-in sequence types), lists can be indexed and sliced:

```py
In [3]: squares[0] # indexing returns the item                                             
Out[3]: 1

In [4]: squares[-1]                                            
Out[4]: 25

In [5]: squares[-3:] # slicing returns a new list                                 
Out[5]: [9, 16, 25]
```

All slice operations return a new list containing the requested elements. This means that the following slice returns a shallow copy of the list:

```py
In [6]: squares[:]                                            
Out[6]: [1, 4, 9, 16, 25]
```

Lists also support operations like concatenation:

```py
In [7]: squares + [36, 49, 64, 81, 100]                       
Out[7]: [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

Unlike strings, which are immutable, lists are a mutable type, i.e. it is possible to change their content:

```py
In [8]: cubes = [1, 8, 27, 65, 125]  # something's wrong here 

In [9]: 4 ** 3 # the cube of 4 is 64, not 65!                                                
Out[9]: 64

In [10]: cubes[3] = 64 # replace the wrong value                                        

In [11]: print(cubes)
[1, 8, 27, 64, 125]
```

You can also add new items at the end of the list, by using the append() method:

```py
In [13]: cubes.append(216) # add the cube of 6                                    

In [14]: print(cubes)                                         
[1, 8, 27, 64, 125, 216]
```

The built-in function len() also applies to lists:

```py
>>> letters = ['a', 'b', 'c', 'd']
>>> len(letters)
4
```

[More](https://docs.python.org/3.8/tutorial/introduction.html#lists)