# Couchbase Development Workshop

This repository contains the material for a combined developer workshop. The following SDK-s are covered:

* C/C++
* Java


# Requirements

Each training computer should have at least the following HW configuration

* 4 CPU cores >=2GHz
* 8 GB RAM
* 50 GB free disk space

The following connectivity is expected:

* Internet access
* Access to Dropbox (alternatively the training material and environment can be provided on a network share in the LAN)

The following software needs to be installed on the attendee's computer:

* VirtualBox >= 4.3

The attendee should have all required permissions to create Virtual Machines and Virtual Machine networks on his box.


# Virtual Machine Setup

> Instead of setting up 4-5 VM-s, we will set up exactly 1 VM which will include all required components.

If you use the provided VM image, then you can skip the following steps:

* Create 64 Bit Linux VM in VirtualBox and call it 'Couchbase-Dev'
* Assign 3072 MB RAM to it
* Assign a 25GB disk to it
* Change the CPU configuration to use at least 2 cores of your host machine
* Add the media 'CentOS-7-x86_64-DVD-1611.iso' (The DVD CentOS7 media from https://www.centos.org/download/)
* Start the VM, choose 'Install' and follow the installation instructions
* Set the root password to 'couchbase'
* Choose the 25GB disk with automatic partitioning
* Choose to create a user 'couchbase' and password 'couchbase' during the installation
* Wait for the installation to complete

## Configure the VM network

### NAT

The NAT interface should be there by default. The NAT IP is usually something like '10.0.2.15'. 

In order to enable access from the outside world via NAT, port forwarding can be used. So to simplify further configuration steps it makes sense to allow the access from the outside world to the VM via NAT and port forwarding. Under the network settings of the VM's NAT network define the following port forwardings:

| Name          | Host port        | Gest port |
| ------------- |------------------|---------- |
| SSH           |9122              | 22        |
| CB            |9191              | 8091      |
| VNC           |9159              | 5901      |

Boot the VM and disable the firewall:
```
systemctl disable firewalld
systemctl stop firewalld
```

## Host only

The next step is to allow the machine to be connected by other machines in the network because in the exercises we want build a cluster of VM-s here. First we need to add a second network adapter:

* Power off the VM
* Under the VM settings add 'Adapter 2' and enable it
* Select 'Host-only Adapter' as the type
* If there is no global host-only network then you need to create it via the general Virtualbox preferences
* Power on the maching

## Network settings

Your VM should now have two network cards. You can double check and change the settings by using the following tool:

```
nmtui
```

* Check the name server settings
* Change the host name to 'couchbase-dev.localdomain'


