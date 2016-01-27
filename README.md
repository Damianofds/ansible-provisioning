# ansible-provisioning
An ansible custom role to install PostGIS + a playbook which uses [this](https://github.com/silpion/ansible-tomcat) and [this](https://github.com/silpion/ansible-java) awesome  roles to install tomcat and java.

## Usage

* Install python and other related stuff, ansible 1.9.4, vagrant and vbox (see below for the istructions and required sw version)
* clone this repo 
* run ``vagrant up`` on the root folder of the repo
or
* add your ip list in the ``hosts`` file and run ``sudo ansible-playbook -vvvv -i hosts playbook.yml -u vagrant -k`` (no -k option if you use a SSH key)

## Install python stuff
In order to run ansible we need for python 2.7 which comes out of the box in ubuntu 2.7.
Anyways we have to install a couple of other python related packages

```
# psycopg2 is requested by the ansible postgres module we use in this playbook
#/$ sudo apt-get install python-psycopg2 
# run this to update the jinja package... we need jinja >= 2.7 and by default is 2.6 on ubuntu
#/$ sudo apt-get install libpq-dev python-dev
# install pip because it's cool
#/$ sudo apt-get install python-pip
# check the jinja package version to be sure
#/$ pip freeze | grep Jinja2
Jinja2==2.7.3
```

## Install ansible 1.9.4 on Ubuntu 12.04 LTS

First, install ansible as suggested onthe official website:
```
#/$ sudo apt-get install software-properties-common
#/$ sudo apt-add-repository ppa:ansible/ansible
#/$ sudo apt-get update
#/$ sudo apt-get install ansible
```
But wait, we have installed ansible >= 2.0 we want 1.9.4! so let's purge it
```
#/$ sudo apt-get purge ansible
```

now we have the ansible dependencies installed, let's go to install ansible 1.9.4 using the .deb in this repo
```
#/$ cd ansible-binaries
#ansible-binaries/$ sudo dpkg -i ansible_1.9.4-1ppa~precise_all.deb
#ansible-binaries/$ ansible --version
ansible 1.9.4
```

## Install vagrant and vbox
Ubuntu precise repo has a too old version of vagrant, let's install it using the deb pkg on the vagrant website
```
#/$ cd /tmp
#tmp/$ wget https://releases.hashicorp.com/vagrant/1.7.4/vagrant_1.7.4_x86_64.deb
#tmp/$ dpkg -i vagrant_1.7.4_x86_64.deb
#tmp/$ vagrant --version
Vagrant 1.7.4
```
Virtual should be already installed on ubuntu 12 desktop, if not
```
#tmp/$ sudo apt-get install virtualbox-qt
```
