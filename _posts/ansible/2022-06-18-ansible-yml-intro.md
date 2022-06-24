---
layout: single
title:  "Part 07: Ansible YAML Introduction"
date:   2022-06-18 09:55:00 +0500
categories: ansible
tags:
  - automation
  - yaml
toc: true
toc_label: "On This Post"
toc_sticky: true
---

## Ansible and YAML
[YMAL](https://yaml.org/) YAML is the abbreviated form of “YAML Ain’t markup language” is a data serialization language which is designed to be human -friendly and works well with other programming languages for everyday tasks.

Yaml is a less complex than XML or JSON and it allows you to provide configuration settings.

### YAML Basic Rules

- YAML files should end in .yaml or .yml
- YAML is case sensitive
- YAML does not allow the use of tabs, spaces are used instead of tabs.
- '#' is uesd as comments
- YAML files are supposed to start with three dashes `---`

### YAML Basic Data Types

1. In general, YAML strings don’t have to be quoted, although you can quote them if you prefer. Even if there are spaces, you don’t need to quote them.
2. In some scenarios in Ansible, you will need to quote strings. These typically involve the use of {{ braces }} for variable substitution.
3. YAML has a native Boolean type and provides you with a wide variety of strings that can be interpreted as true or false, and not case sensitive.

`true` or `True` and `false` or `False`

#### Scalers

Scalers is a single value and a variable, it can be string, integer or bool.

```yml
max_retry: 100 # int
database: 'users' #string
pass: true # bool
date: 1990-02-06 14:33:22 # ISO 8601 standard
```

#### Mapping

YAML dictionaries are like objects in JSON, dictionaries in Python, or hashes in Ruby. Technically, these are called mappings in YAML, but I call them dictionaries here to be consistent with the official Ansible documentation. They look like this:

```yml
animals:
  name: cat
  age: 5
```

#### Sequence

YAML lists are like arrays in JSON and Ruby or lists in Python. Technically, these are called sequences in YAML, but I call them lists here to be consistent with the official Ansible documentation. They are delimited with hyphens, like this

```yml
# list
employee:
  - name: Jack
  - name: Syd
# list
employee: ["Jack", "Syd"]  
# complex list
employee:
  - name: Jack
    age: 28
  - name: Syd
    age: 34
# complex list    
employee:
  - {name: "Jack", age: "22"}
  - {name: "Syd", age: "42"}
```

### Line Folding

When writing playbooks, you’ll often encounter situations where you’re passing many arguments to a module. You might want to break this up across multiple lines in your file, but you want Ansible to treat the string as if it were a single line.

For example:

```yml
employee:
  - name: Jack
    age: 28
# This is a single line 
description: > 
  This is 1st line
  this is a 2nd line
  this is a 3rd line
```

You can also do this with YAML by using the ( | ) character. The YAML parser will place line breaks.

```yml
# not a sigle line
signature: |
  Mike
  Academy
  E-mail - abc@abc  
```

See more on [YAML](https://www.tutorialspoint.com/yaml/index.htm)
