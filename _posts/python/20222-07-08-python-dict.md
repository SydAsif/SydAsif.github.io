---
layout: single
title:  "Python: Python Dictionary"
date:   2022-07-08 11:02:15 +0500
categories: python
tag: python
toc: true
toc_label: "On This Post"
toc_sticky: true
---

## Introduction
Dictionaries are used to store data in key:value pairs. A dictionary is a collection which is ordered, changeable and do not allow duplicates.

- Dictionaries are written with curly brackets, and have keys and values:

```py
In [1]: my_dict = { 
   ...:     "name": "Mike", 
   ...:     "age": 42, 
   ...:     "qualification": "B.A", 
   ...:     "post": "Engineer" 
   ...: }                                                                       

In [2]: print(my_dict)                                                          
{'name': 'Mike', 'age': 42, 'qualification': 'B.A', 'post': 'Engineer'}
```

- Dictionary items are presented in key:value pairs, and can be referred to by using the key name.

```py
In [3]: print(my_dict["name"])                                                  
Mike
```

- There is also a method called get() that will give you the same result:

```py
In [4]: print(my_dict.get("age"))                                               
42
```

- Dictionaries are changeable, meaning that we can change, add or remove items after the dictionary has been created.

```py
In [5]: my_dict["education"] = "M.A" 
   ...: print(my_dict)                                                          
{'name': 'Mike', 'age': 42, 'qualification': 'B.A', 'post': 'Engineer', 'education': 'M.A'}
```

- The pop() method removes the item with the specified key name:

```py
In [6]: my_dict.pop("education") 
   ...: print(my_dict)                                                          
{'name': 'Mike', 'age': 42, 'qualification': 'B.A', 'post': 'Engineer'}
```

- The del keyword removes the item with the specified key name:

```py
In [7]: del my_dict["age"] 
   ...: print(my_dict)                                                          
{'name': 'Mike', 'qualification': 'B.A', 'post': 'Engineer'}
```

- The update() method will update the dictionary with the items from the given argument. The argument must be a dictionary, or an iterable object with key:value pairs.

```py
In [8]: my_dict.update({"location": "Pakistan"}) 
   ...: print(my_dict)                                                          
{'name': 'Mike', 'qualification': 'B.A', 'post': 'Engineer', 'location': 'Pakistan'}
```

- The keys() method will return a list of all the keys in the dictionary.

```py
In [9]: print(my_dict.keys())                                                             
dict_keys(['name', 'qualification', 'post', 'location'])
```

- The values() method will return a list of all the values in the dictionary.

```PY
In [10]: print(my_dict.values())                                                          
dict_values(['Mike', 'B.A', 'Engineer', 'Pakistan'])
```

- The items() method will return each item in a dictionary, as tuples in a list.

```PY
In [11]: print(my_dict.items())                                                           
dict_items([('name', 'Mike'), ('qualification', 'B.A'), ('post', 'Engineer'), ('location', 'Pakistan')])
```

- You can loop through a dictionary by using a for loop. When looping through a dictionary, the return value are the keys of the dictionary, but there are methods to return the values as well.

```PY
In [12]: for x in my_dict: 
    ...:     print(x) 
    ...:                                                                                  
name
qualification
post
location
```

- You can use the keys() method to return the keys of a dictionary:

```PY
In [13]: for x in my_dict.keys(): 
    ...:     print(x) 
    ...:                                                                                  
name
qualification
post
location
```

Print all values in the dictionary, one by one:

```PY
In [14]: for x in my_dict: 
    ...:     print(my_dict[x]) 
    ...:                                                                                  
Mike
B.A
Engineer
Pakistan
```

- You can also use the values() method to return values of a dictionary:

```PY
In [15]: for x in my_dict.values(): 
    ...:     print(x) 
    ...:                                                                                  
Mike
B.A
Engineer
Pakistan
```

- Loop through both keys and values, by using the items() method:

```PY
In [16]: for k, v in my_dict.items(): 
    ...:     print(k, v) 
    ...:                                                                                  
name Mike
qualification B.A
post Engineer
location Pakistan
```

- Create a dictionary that contain three dictionaries:

```PY
my_family = {
  "child1" : {
    "name" : "Emil",
    "year" : 2004
  },
  "child2" : {
    "name" : "Tobias",
    "year" : 2007
  },
  "child3" : {
    "name" : "Linus",
    "year" : 2011
  }
}
```

## Dictionary Methods

Python has a set of built-in methods that you can use on dictionaries.

```py
#Method Description
clear() # Removes all the elements from the dictionary
copy() # Returns a copy of the dictionary
fromkeys() # Returns a dictionary with the specified keys and value
get() # Returns the value of the specified key
items() # Returns a list containing a tuple for each key value pair
keys() # Returns a list containing the dictionary's keys
pop() # Removes the element with the specified key
popitem() # Removes the last inserted key-value pair
setdefault() # Returns the value of the specified key. If the key does not exist: insert the key, with the specified value
update() #Updates the dictionary with the specified key-value pairs
values() # Returns a list of all the values in the dictionary
```
