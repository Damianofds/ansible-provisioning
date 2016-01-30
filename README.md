# ansible-provisioning
Install PostGIS, java and 2 tomcat instances on a vagrant VM or on your own production VM

This repo contanis an ansible role to install PostGIS on ubuntu 12.04.

The playbook in ``playbook.yml`` use that role to install postgis and [this](https://github.com/silpion/ansible-tomcat) and [this](https://github.com/silpion/ansible-java) awesome roles to install java and 2 tomcat instances.

## Usage

See below to **Setting up the control machine**.

after you setup your control machine:

* clone this repo (the repo root dir is indicated with **#~/repo-root$**)
* install the roles for java and tomcat running ``#~/repo-root$ sudo ansible-galaxy install -r requirements.yml``

then you have two options:

* run ``#~/repo-root$ vagrant up`` on the root folder of the repo

**or**

* add your ip list in the ``hosts`` file and run ``#~/repo-root$ sudo ansible-playbook -vvvv -i hosts playbook.yml -u vagrant -k`` (no -k option if you use a SSH key) to deploy your own production virtual machines.

## Setting up the control machine

Assuming that you are going to setup an ubuntu 12.04.5 machine from a fresh installation you need to install 3 main things:
* **python and its other related stuff**
* **ansible 1.9.4**
* **vagrant and vbox** only if you wanna use vagrant pf course

but before ensure to have apt.cache updated and some basics tools installed:

```
#~/$ sudo apt-get update
#~/$ sudo apt-get install git vim curl
#There's some shit in the repo useful to setup the control machine, so let's clone it now
#~/$ git clone https://github.com/Damianofds/ansible-provisioning.git
```

### Install python stuff
In order to run ansible we need for python 2.7 which comes out of the box in ubuntu 2.7.
Anyways we have to install a couple of other python related packages

```
# install pip because it's cool and we are going to use it
#~/$ sudo apt-get install python-pip
# psycopg2 is requested by the ansible postgres module we use in this playbook
#~/$ sudo apt-get install python-psycopg2 
# run this command to update the jinja package... we need jinja >= 2.7 and by default is 2.6 on ubuntu
#~/$ sudo pip install jinja2 --upgrade
# check the jinja package version to be sure
#~/$ pip freeze | grep Jinja2
Jinja2==2.8
#/$ sudo apt-get install libpq-dev python-dev

```

### Install ansible 1.9.4 on Ubuntu 12.04 LTS

First, install ansible as suggested onthe official website:
```
#~/$ sudo apt-get install software-properties-common
#~/$ sudo apt-add-repository ppa:ansible/ansible
#~/$ sudo apt-get update
#~/$ sudo apt-get install ansible
```
But wait, we have installed ansible >= 2.0 we want 1.9.4! so let's remove it
```
#~/$ sudo apt-get remove ansible
```

now we have the ansible dependencies installed, let's go to install ansible 1.9.4 using the .deb in this repo
```
#~/repo-root$ cd ansible-binaries
#~/repo-root/ansible-binaries/$ sudo dpkg -i ansible_1.9.4-1ppa~precise_all.deb
#~/repo-root/ansible-binaries/$ ansible --version
ansible 1.9.4
```

### Install vagrant and vbox
Ubuntu precise repo has a too old version of vagrant, let's install it using the deb pkg on the vagrant website
```
#/$ cd /tmp
#tmp/$ wget https://releases.hashicorp.com/vagrant/1.7.4/vagrant_1.7.4_x86_64.deb
#tmp/$ sudo dpkg -i vagrant_1.7.4_x86_64.deb
#tmp/$ vagrant --version
Vagrant 1.7.4
```
Virtual should be already installed on ubuntu 12 desktop but it's a 4.1.x version..
let's install oracle vbox version 5.x, first of all purge all the existing vbox packages
```
#tmp/$ sudo apt-get purge virtualbox-qt
```
then follow the instructions for Debian/Ubuntu on the [official vbox website](https://www.virtualbox.org/wiki/Linux_Downloads)

Ah and the default box loaded with vagrant is a 64 bit OS so if you get some generic errors from the vagrant provider be sure to have VT-x extensions enabled on your control machine!
