---
layout: single
title:  "Part 04: Docker for Networking"
date:   2022-07-20 12:48:15 +0500
categories: docker
tags: 
  - automation
  - python
toc: true
toc_label: "On This Post"
toc_sticky: true
---

## Network Automation lab With Docker
In this lab tutorial, we will connect our container to a network in GNS3 to test our [previously created docker container](https://sydasif.github.io/docker/docker-networking/#build-your-own-container), but first, we will create our lab in GNS3.

## Lab Setup

We will create simple network topology in GNS3 as below:

![LAb TOPOLOGY](/assets/images/docker.png)

1. Open GNS3 and add a cisco router and switch.
2. Add cloud to your topology, but make sure to chose your host server, not GNS3VM as below:

![PIC](/assets/images/ubuntu.png)

After that, double click on cloud node to configure docker0 interface:

![PIC](/assets/images/docker0.png)

In above configuration tab check _show special ethernet interface_, select docker0 from dropdown menu click add, apply and ok.

### Router configuration

Configure router as below:

```console
conf t
!
hostname R1
!
enable secret 5 $1$NS47$q9v1kBxcavk6vCzCGNmTH1
!
no ip domain lookup
ip domain name tech.com        
!
username admin privilege 15 password 0 cisco
!
interface FastEthernet0/0
 ip address 172.17.0.10 255.255.0.0
 duplex auto
 speed auto
!
line vty 0 4
 logging synchronous
 login local
!
!
end
```

We learn about Docker [Networking tutorial](https://sydasif.github.io/docker/docker-networking-lab/#networking-tutorials) in our Part 03, So we configure router interface in the same subnet as our docker0 interface at our host machine as below:

```console
╭─$ ~  
╰─➤  ip addr show | grep docker0
docker0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
```

### Testing Python script

In this step we test our already created container to run our script as below:

- Start container.

```console
╭─$ ~  
╰─➤  docker start netmiko                 
netmiko
```

- Run Python script.

```console
╭─$ ~  
╰─➤  docker exec -it netmiko python app.py
Interface                  IP-Address      OK? Method Status                Protocol
FastEthernet0/0            172.17.0.10     YES NVRAM  up                    up      
FastEthernet0/1            unassigned      YES NVRAM  administratively down down 
```

- stop the container.

```console
╭─$ ~  
╰─➤  docker stop netmiko                  
netmiko
```

- remove the containers.

```console
╭─syd@ubuntu ~  
╰─➤  docker rm netmiko 
netmiko
```

That's it, we run our script successfully in lab environment.
