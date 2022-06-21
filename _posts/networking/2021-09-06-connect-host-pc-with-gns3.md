---
layout: single
title:  "How to Connect Window Host PC (Win 10) with GNS3"
date:   2021-09-06 11:50:00 +0500
categories: networking
tags: 
  - cisco
  - gns3
toc: true
toc_label: "On This Post"
toc_sticky: true
---

## How to Connect Windows Host PC with Your Device in  GNS3

In this tutorial, I'm teaching you how to connect GNS3 topology with your Windows host machine. We are using a Microsoft loopback adapter for this lab which simplifies the management of network devices in GNS3. The required steps for this lab is described below:

1. [GNS3](https://www.youtube.com/watch?v=Ibe3hgP8gCA) and [VMware](https://www.youtube.com/watch?v=A0DEnMi09LY)
2. Download the [PuTTY.exe](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) file.
3. Install Microsoft loopback adapter and GNS3 configuration.
4. Configuration of the network device.
5. Configuration of windows defender firewall.

### Install the Microsoft loopback adapter

1. Right-click on the window start menu icon and select **Device Manager**. The device manager window will immediately open (or you may use any other way how to open the device manager window)
2. Click on **Action**, and select **Add legacy hardware**
3. SClick **Next** on the welcome screen
4. Choose **"Install the hardware that I manually select from a list"** and click on **Next**
5. Scroll down and select **Network adapters** from offered common hardware types and click on **Next**
6. Select **Microsoft** as the manufacturer, and then select **Microsoft KM-TEST** Loopback adapter card model, click on **Next**
7. Click on **Next**
8. Click on **Finish**  and identify your loopback adaptor, in my case Ethernet2 as shown below:

![picture](/assets/images/loopback.png)

### Configuration of GNS3 and network device

Start GNS3 and drop a cloud node at the workspace and configure as below:

1. Right-click Cloud node, select Configure, and then select “Show special Ethernet interfaces.”
2. Add the Ethernet2 from the drop-down menu.
3. Delete any other interfaces.
4. Highlight the Ethernet2
5. Click on add button.
6. Apply ok.
7. Change the symbol to a computer and rename cloud node to **PC**.

![picture](/assets/images/cloud%20.png)

Configure Ethernet2 adaptor from opening windows Network and Sharing Centre then change adopter setting and add static IP address as above. The IP address used in this example is only for the lab.

![picture](/assets/images/ip%20setting.png)

Add switch and router as below:

![lab](/assets/images/lab.png)

- Switch1 is optional and required no configuration.
- Configure SW1 as below:

```console
conf t
!
hostname SW1
!
enable secret cisco
service password-encryption
!
username admin password cisco
!
no ip domain-lookup       
!
interface Vlan1
 ip address 9.9.9.2 255.255.255.0
 no shutdown
!
line vty 0 4
 logging synchronous
 login local
 transport input all
!
end
!
wr
```

Also configure router in same network.

### Configuration of windows defender firewall

1. Open _cmd.exe_ and check connectivity with ping, hope all is well.
2. You can open the Windows Defender firewall as shown.
3. Open Windows defender firewall with Advanced Security and enable these two settings on the inbound rules as below:

![picture](/assets/images/firewall-%20rule.png)

   1. File and Printer Sharing (Echo Request – ICMPv4-In) Private
   2. File and Printer Sharing (Echo Request – ICMPv6-In) Private

This will allows GNS3 to send back ICMP (ping) request to the host PC.
