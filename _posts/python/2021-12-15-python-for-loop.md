---
layout: single
title:  "Python: for loop"
date:   2021-12-15 15:02:15 +0500
categories: python
tag: python
toc: true
toc_label: "On This Post"
toc_sticky: true
---

## for loop in python
Python’s for statement iterates over the items of any sequence (a list or a string), in the order that they appear in the sequence. For example:

```py
In [6]: # Measure some strings:                                                 

In [7]: words = ['cat', 'window', 'door']                                       

In [8]: for w in words: 
   ...:     print(w) 
   ...:                                                                         
cat
window
door
```

## The range() Function

If you do need to iterate over a sequence of numbers, the built-in function range() comes in handy.

```py
In [1]: subnet = "192.168.10."                                                  

In [2]: for i in range(5): 
   ...:     print(subnet + str(i)) 
   ...:                                                                         
192.168.10.0
192.168.10.1
192.168.10.2
192.168.10.3
192.168.10.4
```

The given end point is never part of the generated sequence; range(10) generates 10 values, the legal indices for items of a sequence of length 10. It is possible to let the range start at another number, or to specify a different increment (even negative; sometimes this is called the ‘step’).

```python
range(5, 10)
   5, 6, 7, 8, 9

range(0, 10, 3)
   0, 3, 6, 9

range(-10, -100, -30)
  -10, -40, -70
```

We can use for loop, nested as follows:

```python
In [3]: device = ['r1', 'r2', 'r3']                                             

In [4]: fqdn = ['cisco.com']                                                    

In [5]: for d in device: 
   ...:     for n in fqdn: 
   ...:         print(d + '.' + n) 
   ...:                                                                         
r1.cisco.com
r2.cisco.com
r3.cisco.com
```

See more on [python-doc](https://docs.python.org/3.8/tutorial/controlflow.html#for-statements).
