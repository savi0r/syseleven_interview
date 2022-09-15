# OpenStack Trial Day Challenge

Hello and welcome to the trial day challenge! First of all, we would like to
thank you for participating, and would really appreciate your honest feedback.

We wish that you have some fun today, and we are always there for you if you
have any questions.

Good luck!

## Objective

You are provided with credentials for an OpenStack account in our production
public cloud. There is another OpenStack cluster deployed on virtual machines in
this account. This OpenStack-in-OpenStack cluster is your lab environment, in
which you can accomplish all trial day goals. You are also provided with an
Ansible automation, that is used to deploy this lab OpenStack-in-OpenStack
cluster.

This challenge is not closed-book. You are welcome to talk to us and discuss
anything, like you would do in real daily work. You can even approach this by
doing pair programming with us, if you wish to. You can discuss any ideas with
us before you start to implement them. Of course you don't have to, and if you
like to focus by yourself, please feel free to do so. You can use Google, or any
other documentation sources.

The goal of this challenge is not to check if you have right or wrong solutions
to tasks, but rather to get the understanding how you work, and which approaches
you take.

The tasks are at the very bottom of this document, feel free to jump there
directly, or keep reading to get some details about lab environment.

## Accessing lab cluster VMs

Use these environment variables to get API acccess to our production cluster,
where your lab OpenStack-in-OpenStack is deployed in virtual machines.

```
export OS_AUTH_URL=https://keystone.cloud.syseleven.net:5000/v3
export OS_IDENTITY_API_VERSION=3
export OS_PROJECT_NAME=syseleveneigenbedarf-syseleven-probetag-projekt-2
export OS_USER_DOMAIN_NAME=Default
export OS_PROJECT_DOMAIN_NAME=Default
export OS_INTERFACE=public
export OS_ENDPOINT_TYPE=public
export OS_USERNAME=probetag2@syseleven.de
export OS_PASSWORD=KM8bljFDjXfebkaFCiStJ
export OS_REGION_NAME=fes
```

There is a jumphost VM pre-deployed for your needs too. It is called
`workstation01.openstack-lab.local`. Access it via SSH on the IP
address 195.192.154.199. Username is `ubuntu`, and you will also need this SSH
private key:

```
-----BEGIN OPENSSH PRIVATE KEY-----
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
-----END OPENSSH PRIVATE KEY-----
```

The jumphost VM has everything that you need, like Ansible and OpenStack CLI
client. Feel free to install anything else you need with `apt`. This lab
environment is 100% yours and will be destroyed afterwards.

You can SSH to any other VM from the jumphost VM with the same credentials.

## Accessing lab cluster API and dashboard

For this, you will have to use SSH with port forwarding.

```
ssh 195.192.154.199 -A -l ubuntu -L 8088:lb01.openstack-lab.local:8088 -L 6082:controller01.openstack-lab.local:6082
```

After sucessful connection, the dashboard will be available on http://localhost:8088.

If you need API access to the lab OpenStack-in-OpenStack cluster, then OpenStack
cli client is installed on all VMs, and credentials can be found in
`/etc/openstack/admin-openrc.sh`,

Username and password are `admin`.

## Lab automation

Ansible code which is part of this repository is pre-deployed for you in
`~/automation` directory on the jumphost. Please make sure to work with this
repository when you implement solutions for your task. We would like to see some
Git history in this repository with your changes.

To run the whole Ansible play, simply execute following commands in the
automation directory. Make sure that your `OS_` variables with credentials for
our production OpenStack are set, because Ansible will need them to get
information about running VMs. For your convenience, these variables are saved
in `~/OpenStack-lab-credentials.sh`. Don't confuse these with inner
OpenStack-in-OpenStack credentials, which look similar but stored in
`/etc/openstack/admin-openrc.sh`.

```
cd automation
source ~/OpenStack-lab-credentials.sh
ansible-playbook -i lab.ini ./lab.yml
```

# Lab cluster description

You have some objects like network, router, security group and SSH key
preconfigured for you in the Lab OpenStack-in-OpenStack environment. Also, there
are some VMs running. Feel free to do anything you want with these objects if
you need to. You can delete VMs that are already running. Private part of the
pre-configured SSH key is the same that is used to access lab VMs and can be
found in this document.

## Starting VMs in lab cluster and accessing them

Please note that this whole setup is 100% virtual and running on cheap virtual
machines in our production OpenStack cloud. This is why we do not recommend to
run heavy VMs like Ubuntu. Instead, you are provided with a Cirros Linux image.
This OS is perfect for labs like this. It takes around 50 megabytes of disk
space, has very basic tools like ping, traceroute and SSH. It not only runs SSH
server by default, but also provides console with a login and password, so it is
possible to use the VM even without network or when SSH key was not properly
deployed.

## Internet access from lab cluster

There is an external `provider` network pre-configured for you. You can obtain
floating IP addresses from it. They should be reachable from any VM, including
jumphost. These IP addresses are not reachable from the Internet, but you can
reach Internet resources from VMs thanks to NAT.

# Tasks

## Task 1: Troubleshooting

We broke something in the lab OpenStack-in-OpenStack cluster. Let's see if you
can figure out what is wrong there.

Your imaginary customer reports that sometimes when they start a bunch of new
VMs for their highly available Galera database, they cannot SSH into some of
them. According to the customer ticket, a "Permission denied" error is displayed
in verbose SSH client output. Customers also notice that recreating failed VM
from scratch will usually help, but not always.

Your goal is to figure out what is going on, and when possible, provide a
solution. Imagine that it is a regular working day and we are talking about a
real customer ticket.

## Task 2: Configuration

The lab OpenStack cluster is missing OpenStack volume service. Add this service
to the cluster, so VMs can have some volumes attached to them. Try to integrate
volume service to existing lab infrastructure, and automate it properly.

It is your task to understand how existing automation works, how services are
deployed in the lab cluster, how service discovery works, and how to add a new
service.

Be prepared to present your volume service implementation to us. Extra points
are awarded, if you describe how existing automation works, and what are pros
and cons of choosen approach.

# Something is wrong or does not work?

**Just talk to us!** Our Google Meet channel is https://meet.google.com/hhi-vped-qvk

# Do you like this OpenStack lab?

Then take this repo with you, all files here are copyleft. If you publish it in
Internet however, please mention SysEleven GmbH as an author. Nothing in this
lab automation reflects our real infrastructure, secrets, or know-hows.
