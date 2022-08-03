---
layout: single
title:  "Vagrant with VMware Workstation"
date:   2022-08-02 15:02:15 +0500
categories: networking
tags: 
  - automation
  - vagrant
toc: true
toc_label: "On This Post"
toc_sticky: true
---

## Introduction
Vagrant is for virtual machines what Docker is for containers. Vagrant is a wrapper for different hypervisor programs like VMware Workstation Pro, VMware Player, VirtualBox, Hyper-V, VMware vSphere, etc. Vagrant uses a simple text-based configuration file called Vagrantfile to quickly set up a development environment with one of the supported virtual machine providers/hypervisors.

In this article, I will show you how to install the latest version of Vagrant on Ubuntu 20.04 LTS and configure Vagrant to use VMware Workstation Pro 16 as a virtual machine provider. So, let’s get started.

## Installing Required Dependencies

First, update the APT package repository cache as follows:

```console
sudo apt update
```

To install curl, run the following command:

```console
sudo apt install curl -y
```

## Installing Vagrant

First, download the HashiCorp GPG key and add it to the APT package manager with the following command:

```console
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
```

Add the official Vagrant package repository to the APT package manager with the following command and install vagrant:

```console
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt update && sudo apt install vagrant
```

At this point, the latest version of Vagrant should be installed. see [website](https://www.vagrantup.com/downloads) for other Operating systems.

Once Vagrant is installed, you should be able to run the vagrant command from the command-line as any other command.

```console
vagrant --version
```

## Installing Vagrant VMware Utility

To use VMware Workstation Pro 16 with Vagrant, you must install the Vagrant VMware Utility.

To download the latest version of Vagrant VMware Utility, navigate to the link [VMware Utility Downloads](https://www.vagrantup.com/vmware/downloads)

- Once the page loads, click on Debian > 64-bit.
- Your browser should prompt/download the vagrant-vmware-utility-*.deb.
- Now, navigate to the ~/Downloads directory with `cd ~/Downloads` command.

The vagrant-vmware-utility_1.0.20_x86_64.deb package file that you’ve just downloaded should be here. To install the vagrant-vmware-utility_1.0.20_x86_64.deb package file, run the following command:

```console
sudo apt install ./vagrant-vmware-utility_1.0.20_x86_64.deb
```

The APT package manager should start installing the vagrant-vmware-utility_1.0.20_x86_64.deb package.Once you have installed Vagrant and Vagrant VMware Utility, you can easily install the Vagrant plugin vagrant-vmware-desktop with the following command:

```console
vagrant plugin install vagrant-vmware-desktop
```

At this point, the Vagrant plugin vagrant-vmware-desktop should be installed. See [VMware Provider Page](https://www.vagrantup.com/docs/providers/vmware/installation) for latest information.

## Using Vagrant with VMware Desktop Provider

Create a new directory, and navigate to the newly created project directory. Now, you need to create a new file _Vagrantfile_, specify the Vagrant Box that you want to use, and configure it using the Vagrantfile. You can find all the available Vagrant Boxes on the official [website](https://app.vagrantup.com/boxes/search?provider=vmware) of Vagrant.

I will use the generic/ubuntu2004 Vagrant Box, it is a Ubuntu 20.04 LTS Vagrant Box. create a new Vagrantfile with the following command:

```console
nano Vagrantfile
```

Type in the following lines of codes in the Vagrantfile.

```ruby
Vagrant.configure("2") do |config|
  config.vm.box = "generic/ubuntu2004"
  config.vm.provider "vmware_desktop" do |vb|
     vb.memory = "1024"
   end
end
```

Once you’re done, press _Ctrl> + X_ followed by _Y_ and _Enter_ to save the Vagrantfile.

To start the Vagrant project, run the command `vagrant up`. Vagrant will download the Vagrant Box generic/ubuntu2004 from the internet as you’re using this Vagrant Box for the first time.

Once the Vagrant Box is downloaded, Vagrant should create the required virtual machines for the project. That’s how you use Vagrant with VMware, if encounter any problem reboot your ubuntu machine will fix the issue.

See [Vagrant Commands Page](https://www.vagrantup.com/docs/cli) for more _cli's_ options.
