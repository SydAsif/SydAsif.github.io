---
layout: single
title:  "Ansible Lab setup with Vagrant"
date:   2022-08-04 11:41:00 +0500
categories: networking
tags: 
  - automation
  - vagrant
toc: true
toc_label: "On This Post"
toc_sticky: true
---

## Introduction
Ansible is an open-source, powerful, and simple tool for client-server and network device automation. Ansible is agent-less, which means nothing to install on a client only Python is installed and SSH is enabled on the remote host.

**How Ansible Works**:- Ansible will do the following.

1. Generate a Python script
2. Copy the script to the remote node
3. Execute the script on a remote node
4. Wait for the script to complete execution on all hosts
5. Remove the script from the remote node

Ansible will then move to the next task in the list, and go through these same steps. It’s important to note the following:

* Ansible runs each task in parallel across all hosts.
* Ansible waits until all hosts have completed a task before moving to the next task.
* Ansible runs the tasks in the order that you specify them.

### Ansible Installation

In this blog, we will create a lab environment using _Vagrant_.

#### Control node requirement

For the control node, you can use any machine with Python 2.7 or Python 3.5 (or higher) installed. The Ansible installation is simple and depends on the OS of your control node, see [Ansible document](https://docs.ansible.com/ansible/2.9/installation_guide/index.html) for installation.

#### Managed node requirement

For managed nodes, Ansible makes a connection over SSH, Python and SSH client is required.

#### Requirements of this lab

1. VMware or Virtual box
2. Vagrant

## Using Vagrant to set up a testing lab

Vagrant is an excellent open-source tool for managing virtual machines. You can use Vagrant to boot a Linux virtual machine inside your laptop, and you can use that as a test server.

I'm using Vagrant for my lab set-up, the process is simple as below:

1. Go to the [Vagrant website](https://www.vagrantup.com/), download the vagrant, and install it on your machine. For more details see [Introduction to Vagrant](https://ayushsharma.in/2021/08/introduction-to-vagrant) and [Quick Start Guide](https://learn.hashicorp.com/tutorials/vagrant/getting-started-index?in=vagrant/getting-started).

2. [Virtual box](https://www.virtualbox.org/wiki/Downloads).

3. Download [Vagrant file](https://gitlab.com/sydasif/my-vagrant-lab/-/tree/main/lab).

Create a directory in your machine and copy the vagrant file from the repo. In my case, I, create a directory in Document, named _lab_ (name can be anything). Open Powershell/Bash and navigate to the _lab_ directory and boot the Vagrant.

### To boot the vagrant devices

```vagrant up``` will create and boot the below devices.

1. centos01
2. ubuntu01

Command after booting to check the status of devices:

```console
╭─$ ~/Desktop/lab  
╰─➤  vagrant status
Current machine states:

centos01                  running (virtualbox)
ubuntu01                  running (virtualbox)

This environment represents multiple VMs. The VMs are all listed
above with their current state. For more information about a specific
VM, run `vagrant status NAME`.
```

Use ```vagrant ssh ubuntu01``` command to ssh into a device and check ping to the other device.
See [Permission Denied](https://stackoverflow.com/questions/36300446/ssh-permission-denied-publickey-gssapi-with-mic) guide on StackOverflow to setup ssh connection.

### Configuring Ansible Client

I have two Vagrant hosts _ubuntu01_, _centos01_ and Ansible _control node_(my pc). On the control node, edit the host's file for IP to name resolution.

```console
sudo nano /etc/hosts
```

After opening the file add below IP and hostname.

```console
192.168.56.10  centos01
192.168.56.11  ubuntu01
```

Create an SSH key on Ansible _control node_ as below and accept the defaults.

```console
ssh-keygen
```

list the keys to verify with the _ls .ssh_ command, and copy the key to the client's machine.

```console
ssh-copy-id -i .ssh/id_rsa.pub vagrant@ubuntu01
ssh-copy-id -i .ssh/id_rsa.pub vagrant@centos01
```

Now ssh to Ubuntu01, and configure the managed host, so that it doesn't require a password to get _sudo_ level access.

```console
ssh vagrant@ubuntu01
sudo visudo
```

Go to the bottom of the file and add this line as below:

```console
vagrant ALL=(ALL) NOPASSWD: ALL
```

Also, configure centos so that it doesn't require a password to get root-level access.

```console
ssh vagrant@centos01
su - 
sudo visudo
```

Go to the bottom of the file and add this line as below:

```console
vagrant ALL=(ALL) NOPASSWD: ALL
```

## Ansible installation on Ubuntu

1. Create a virtual environment

```console
╭─$ ~  
╰─➤  virtualenv ansible2.9
created virtual environment CPython3.8.10.final.0-64 in 2567ms
  creator CPython3Posix(dest=/home/syd/ansible2.9, clear=False, no_vcs_ignore=False, global=False)
  seeder FromAppData(download=False, pip=bundle, setuptools=bundle, wheel=bundle, via=copy, app_data_dir=/home/syd/.local/share/virtualenv)
    added seed packages: pip==22.1.2, setuptools==63.1.0, wheel==0.37.1
  activators BashActivator,CShellActivator,FishActivator,NushellActivator,PowerShellActivator,PythonActivator
```

2. Activate the environment.

```console
╭─$ ~  
╰─➤  source ansible2.9/bin/activate
(ansible2.9) ╭─$ ~  
╰─➤
```

3. Upgrade pip

```console
(ansible2.9) ╭─$ ~  
╰─➤  pip list
Package    Version
---------- -------
pip        22.1.2
setuptools 63.1.0
wheel      0.37.1

[notice] A new release of pip available: 22.1.2 -> 22.2.2
[notice] To update, run: pip install --upgrade pip
```

```console
(ansible2.9) ╭─$ ~  
╰─➤  pip install --upgrade pip
Requirement already satisfied: pip in ./ansible2.9/lib/python3.8/site-packages (22.1.2)
Collecting pip
  Using cached pip-22.2.2-py3-none-any.whl (2.0 MB)
Installing collected packages: pip
  Attempting uninstall: pip
    Found existing installation: pip 22.1.2
    Uninstalling pip-22.1.2:
      Successfully uninstalled pip-22.1.2
Successfully installed pip-22.2.2
(ansible2.9) ╭─$ ~  
╰─➤  pip list
Package    Version
---------- -------
pip        22.2.2
setuptools 63.1.0
wheel      0.37.1
```

4. Install Ansible.

```console
(ansible2.9) ╭─$ ~  
╰─➤  pip install ansible==2.9.9
Collecting ansible==2.9.9
  Downloading ansible-2.9.9.tar.gz (14.2 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 14.2/14.2 MB 374.5 kB/s eta 0:00:00
  Preparing metadata (setup.py) ... done
Collecting jinja2
  Downloading Jinja2-3.1.2-py3-none-any.whl (133 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 133.1/133.1 kB 69.9 kB/s eta 0:00:00
Collecting PyYAML
  Downloading PyYAML-6.0-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_12_x86_64.manylinux2010_x86_64.whl (701 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 701.2/701.2 kB 194.6 kB/s eta 0:00:00
Collecting cryptography
  Downloading cryptography-37.0.4-cp36-abi3-manylinux_2_24_x86_64.whl (4.1 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 4.1/4.1 MB 215.1 kB/s eta 0:00:00
Collecting cffi>=1.12
  Downloading cffi-1.15.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (442 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 442.7/442.7 kB 253.7 kB/s eta 0:00:00
Collecting MarkupSafe>=2.0
  Downloading MarkupSafe-2.1.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (25 kB)
Collecting pycparser
  Downloading pycparser-2.21-py2.py3-none-any.whl (118 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 118.7/118.7 kB 143.3 kB/s eta 0:00:00
Building wheels for collected packages: ansible
  Building wheel for ansible (setup.py) ... done
  Created wheel for ansible: filename=ansible-2.9.9-py3-none-any.whl size=16168980 sha256=95256af318d09dbee7bbe604a228af5f82ff2e14d4172b62bdb90d2b78407a0f
  Stored in directory: /home/syd/.cache/pip/wheels/50/cb/af/4945f05738b88f4d5c273e7e2690e832e1fa9edb8461c2b53c
Successfully built ansible
Installing collected packages: PyYAML, pycparser, MarkupSafe, jinja2, cffi, cryptography, ansible
Successfully installed MarkupSafe-2.1.1 PyYAML-6.0 ansible-2.9.9 cffi-1.15.1 cryptography-37.0.4 jinja2-3.1.2 pycparser-2.21
(ansible2.9) ╭─$ ~  
╰─➤  ansible --version
ansible 2.9.9
  config file = None
  configured module search path = ['/home/syd/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /home/syd/ansible2.9/lib/python3.8/site-packages/ansible
  executable location = /home/syd/ansible2.9/bin/ansible
  python version = 3.8.10 (default, Jun 22 2022, 20:18:18) [GCC 9.4.0]
```

To test Ansible installation, run the below command:

```json
$ ansible localhost -m ping

[WARNING]: No inventory was parsed, only implicit localhost is available
localhost | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

### Ansible Configuration Set-Up

Ansible configuration/inventory files define setting/managed nodes that ad-hoc commands/playbooks can be run against. I'm creating ansible.cfg/hosts files in the ansible default location (/etc/ansible).

```console
sudo mkdir /etc/ansible
sudo nano /etc/ansible/ansible.cfg
```

In ansible.cfg we define the location of the inventory file which will be used for this project as follows.

```console
[defaults]
inventory = ./hosts
```

Create groups and add hosts to the group.

```console
[ubuntu]
ubuntu01  

[centos]
centos01

[linux:children]
ubuntu
centos

[linux:vars]
ansible_usr=vagrant
```

The lab setup is now completed.

## [Introduction to ad hoc commands](https://docs.ansible.com/ansible/latest/user_guide/intro_adhoc.html)

An Ansible ad hoc command is a command-line tool to automate a single task on one or more managed nodes. Ad hoc commands are quick and easy, but they are not reusable. Ad hoc commands demonstrate the simplicity and power of Ansible. Ad-hoc system interaction is a powerful and useful tool but some limitations exist.

```json
$ ansible -m ping all
centos01 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
ubuntu01 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```

```json
$ ansible all -a 'whoami'
centos01 | CHANGED | rc=0 >>
vagrant
ubuntu01 | CHANGED | rc=0 >>
vagrant
```

Elevate to root with -b for become. Why? Because Ansible doesn't elevate the _sudo_ privilege by default.

```json
ansible all -b -a 'whoami'
ubuntu01 | CHANGED | rc=0 >>
root
centos01 | CHANGED | rc=0 >>
root
```

Some examples of ad-hoc commands are below:

1. ansible all -a "uptime"
2. ansible all -a "whoami"
3. ansible all -b -a "whoami"

If you do not specify the _-m (module)_, the default _command_ module will run.

```json
ansible all -m command -a 'echo Ansible is fun with Vagrant'
centos01 | CHANGED | rc=0 >>
Ansible is fun with Vagrant
ubuntu01 | CHANGED | rc=0 >>
Ansible is fun with Vagrant
```

It’s a basic command, but a little to explain, the command does the following:

• First, we specify all, so the command will be run across all the inventory we list.

• The -m option is then provided to allow us to specify a module we can use.

• Finally, we specify the -a option allows us to provide arguments to the shell module,
we are simply running an echo command to print the output “Ansible is fun”

If I, remove the _-m command_ from the above ad-hoc command it will also work because ansible uses the _command_ module by default.
  
## Playbook Examples

```yml
---
- name: PLAYBOOK-1        
  hosts: linux
  tasks:
    - name: A UNAME???
      shell: uname -a > /home/vagrant/res.txt

    - name: B WHOAMI???
      shell: whoami >> /home/vagrant/res.txt
```

```json
$ ansible-playbook playbook-1.yaml

PLAY [PLAYBOOK-1] ***************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************
ok: [centos01]
ok: [ubuntu01]

TASK [A UNAME???] ***************************************************************************************************
changed: [centos01]
changed: [ubuntu01]

TASK [B WHOAMI???] **************************************************************************************************
changed: [ubuntu01]
changed: [centos01]

PLAY RECAP **********************************************************************************************************
centos01                   : ok=3    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
ubuntu01                   : ok=3    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0 
```

### Running Multiple Plays

A playbook can have multiple plays and each play can in turn contains multiple tasks.

```yml
---
- name: Play-book to install packages 
  hosts: ubuntu
  become: true
  tasks: 
    - name: Install git on ubuntu
      apt:
        name: git
        state: present


- name: Play-2....
  hosts: centos
  become: true
  tasks:
    - name: Install git on centos
      yum:
        name: git
        state: present
```

```json
ansible-playbook playbook-4.yml

PLAY [Play-1... ubuntu] *********************************************************************************************

TASK [Gathering Facts] **********************************************************************************************
ok: [ubuntu01]

TASK [Install git on ubuntu] ****************************************************************************************
ok: [ubuntu01]

PLAY [Play-2... centos] *********************************************************************************************

TASK [Gathering Facts] **********************************************************************************************
ok: [centos01]

TASK [Install git on centos] ****************************************************************************************
changed: [centos01]

PLAY RECAP **********************************************************************************************************
centos01                   : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
ubuntu01                   : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0 
```

Thanks, for reading.
