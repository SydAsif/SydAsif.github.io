---
layout: single
title:  "Part 05: Ansible YAML Inventory Setting"
date:   2022-06-16 09:55:00 +0500
categories: ansible
tags:
  - automation
  - yaml
toc: true
toc_label: "On This Post"
toc_sticky: true
---

## Ansible Inventory YAML Format
Our last inventory file was the _INI_ format. There is also another format called _.yaml_ or _.yml_ which is more readable and may be required depending on the version of Ansible or module. Therefore, it is a good idea to learn how to create an inventory file in _YAML_ format.

### Default groups

There are two default groups _all_ and _ungrouped_. The _all_ group contains every host. The _ungrouped_ group contains all hosts that don’t have another group aside from all. Every host will always belong to at least 2 groups (_all_ and _ungrouped_ or _all_ and some other group).

There are essential keys that are primarily used in the inventory file in Ansible.

- _children_ to create groups of group
- _hosts_ to add device to the group
- _vars_ to define variables.

Another important point about the _YAML_ file is indentation. This means that all keys and values at the same level must have the same indentation. This is the only way to separate key/value pairs without parentheses or brackets.

Let's first create the groups, add devices and then the variables.

In our previous inventory file, we have **network** as _all_ group, **switch** and **router** as _sub-groups_. So first we create all group, and then with the help of the _“children”_ key and create _sub-groups_ as below:

```yml
  network:
    children:
      switch:
      router:
```

Then we will add devices with the help of _“hosts”_ key in sub-groups.

```yml
  network:
    children:
      switch:
        hosts:
          sw1:
      router:
        hosts:
          r1:
          r2:
```

Lastly, we create variables under the network group with the help of _“vars”_ key.

```yml
---
  network:
    vars:
      ansible_user: admin
      ansible_password: cisco
      ansible_network_os: ios
      ansible_connection: network_cli
    children:
      switch:
        hosts:
          sw1:
      router:
        hosts:
          r1:
          r2: 
```

Above is the result of the inventory file in the format of YAML. You can read more [How to build your inventory](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html) on the website.

In [Part 04](https://sydasif.github.io/ansible/ansible-configuration/) we define the location of the inventory in ansible.cfg as named _hosts_ file, now we changed the file name to _hosts.yml_ to use YAML format inventory file.

```console
[defaults]
inventory = ./hosts.yml 
timeout = 60
host_key_checking = false
```

> Now Ping module result:

```JSON
root@NetworkAutomation-1:~# ansible all -m ping
r2 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
r1 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
sw1 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```
