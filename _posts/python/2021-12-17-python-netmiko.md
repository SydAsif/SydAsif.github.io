---
layout: single
title:  "Python Network Automation with Netmiko"
date:   2021-12-17 15:02:15 +0500
categories: python
tags: 
  - automation
  - gns3
  - python
toc: true
toc_label: "On This Post"
toc_sticky: true
---

## Netmiko
Using telnet in a lab environment for practice or in a fully isolated private network is recommended, but in a production or public network, telnet is vulnerable to cyber attack.

To overcome this anomaly, network engineers use ssh. SSH is a network protocol that is widely used to access and manage a device remotely and a major protocol to access the network devices and servers over the internet.

To automate networking devices via SSH, we will using Netmiko. [Netmiko](https://syd-asif.blogspot.com/2021/09/python-netmiko.html) is a multi-vendor library to simplify Paramiko SSH connections to network devices. Netmiko supports a wide range of devices. These devices fall into three categories.

- Regularly Tested
- Limited Testing
- Experimental

To install netmiko simply use pip for installation.

`pip install netmiko`

Netmiko has the following requirements (which pip will install for you)

- Paramiko >= 2.4.3
- scp >= 0.13.2
- pyserial
- textfsm

We will use our previous topology as below:

![picture](/assets/images/network_automation.png)

[Lab Configuration](https://sydasif.github.io/python/network-automation-gns3/#lab-configuration) same as previous.

## [Example of Netmiko](https://github.com/ktbyers/netmiko/blob/develop/EXAMPLES.md)  

Below is the python code for achieving our task. Write the code using a nano editor as exe_01.py.

```python
# Exercise 1: show ip interface brief using SSH
from netmiko import ConnectHandler

# Create a dictionary representing the device.
cisco_881 = {
    'device_type': 'cisco_ios',
    'host':   '10.10.10.10',
    'username': 'test',
    'password': 'password',
}

# Establish an SSH connection to the device by passing in the device dictionary.
net_connect = ConnectHandler(**cisco_881)

# Execute show commands.
output = net_connect.send_command('show ip int brief')
print(output)
```

> More script at [GitHub](https://github.com/sydasif/network-automation/tree/master/netmiko)
