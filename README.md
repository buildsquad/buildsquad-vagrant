# Vagrant box for buildsquad

This project maintains vagrant-related files for buildsquad runner.

## Installation

### Install Vagrant
This is out of scope, please refer to [the vagrant documentation](http://docs.vagrantup.com/v2/installation/index.html)

### Install Ansible
Again, out of scope, please refer to [the ansible documentation](http://www.ansibleworks.com/docs/gettingstarted.html)
Quickest way is to do that in a virtualenv using [wirtualenvwrapper](http://virtualenvwrapper.readthedocs.org/en/latest/)

```
$ mkvirtualenv ansible
$ workon ansible
$ pip install ansible
```
If `ansible` is installed into the `virtualenv`, you have to activate the `virtualenv` before running `vagrant up`

### Boostrap
You can boostrap the project using the `precise64` default box.

cd to the top level of this project (i.e. where the VagrantFile is) and copy/edit the Vagrantfile

```
$ cp Vagrantfile.sample Vagrantfile
```
then add the box (if using the default one) and run vagrant

```
$ vagrant box add precise64 http://files.vagrantup.com/precise64.box
$ vagrant up
```

This will take a while, but after that you should have all the necessary bits installed.
Now, last step, reboot (to boot with the new kernel) and rerun provision:

```
$ vagrant reload --provision
```

### Known issues

On my laptop (running fedora 19 and vagrant 1.2.4) when running `vagrant up` it fails due to networking not being configured.

The "solution" is to add an ip address for the host machine and rerun provision:

```
$ sudo ip addr add 192.168.111.1/24 dev vboxnet0
$ sudo ip link set vboxnet0 up
$ vagrant provision
```
