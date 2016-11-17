# ansible-provisioning
Install java and tomcat and Geoserver on a redhat target machine

It uses [this](https://github.com/silpion/ansible-tomcat) and [this](https://github.com/silpion/ansible-java) 3rd party roles to install java and tomcat.

## Usage

See below to **Setting up the control machine**. 

**python 2.7**, **jinga2** >= **2.7**, **psycopg2** and  **ansible 1.9.4** are needed! (the tomcat role doesn't work with anisble 2.0 :( ) 

after you setup your control machine:

* clone this repo (the repo root dir is indicated with **#~/repo-root$** in the rest of this doc)

  ``#~/git clone https://github.com/Damianofds/ansible-provisioning.git``
* install the roles for java and tomcat running 
  
  ``#~/repo-root$ sudo ansible-galaxy install -r requirements.yml``

then you have two options:
* run it with vagrant

  ``#~/repo-root$ vagrant up``

**or**

* deploy your own production virtual machines
  * add your ip list in the ``hosts`` file 
  * then run

    ``#~/repo-root$ sudo ansible-playbook -vvvv -i hosts playbook.yml -u vagrant -k``

    (no -k option if you use a SSH key)

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

### Install ansible > 2 on Ubuntu 12.04 LTS

As suggested on the official website:
```
#~/$ sudo apt-get install software-properties-common
#~/$ sudo apt-add-repository ppa:ansible/ansible
#~/$ sudo apt-get update
#~/$ sudo apt-get install ansible
```
