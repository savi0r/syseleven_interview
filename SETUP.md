# Lab Setup

!! This is not for a candidate.

This file just describes how to prepare lab project for you.

## OpenStack Lab Project Setup in UNDERLAY (probetag-eigenbedarf project)

Create a network:
```
openstack network create lab

openstack subnet create --network lab --subnet-range 192.168.128.0/24 --dns-nameserver 1.1.1.1 lab-v4

openstack subnet create --network lab --subnet-pool subnet-pool-v6_1 --ip-version 6 --ipv6-ra-mode dhcpv6-stateless --ipv6-address-mode dhcpv6-stateless --prefix-length 64 lab-v6
```

Create a router:
```

openstack router create lab

openstack router set --external-gateway ext-net lab

openstack router add subnet lab lab-v4
openstack router add subnet lab lab-v6
```

Create a security group:
```
openstack security group create lab
openstack security group rule create --protocol tcp --dst-port 22 --ethertype ipv4 lab
openstack security group rule create --protocol tcp --dst-port 22 --ethertype ipv6 lab
openstack security group rule create --protocol icmp --ethertype ipv4 lab
openstack security group rule create --protocol icmp --ethertype ipv6 lab
openstack security group rule create --remote-group lab lab
```

Create a key:
```
ssh-keygen -f ./lab-key
ssh-add ./lab-key
openstack keypair create --public-key ./lab-key.pub lab
```
Update README.md with the private key generated.


Create a workstation:
```
openstack server create --image <focal> --flavor m1.small --network lab --security-group lab --key-name lab workstation01.openstack-lab.local
openstack server add floating ip workstation01.openstack-lab.local $(openstack floating ip create -f value -c floating_ip_address ext-net)
```
Update README.md with the floating IP address of workstation VM.


## Workstation preparation

SSH into the Workstation VM. Use the key previously created.

Install OpenStack clients, Ansible, Python and Git. Do other initial setup as below:

```
sudo apt update
sudo apt -y upgrade
sudo apt -y install git ansible python3-openstackclient

echo -e 'Host *\n  StrictHostKeyChecking no\n  UserKnownHostsFile /dev/null' > ~/.ssh/config
```

Clone this repository to ~/automation.

```
git clone https://token:<some token>@gitlab.syseleven.de/openstack/all-in-one-lab.git automation
```

Export all `OS_` variables for probetag-eigenbedarf project.

Save these variables to `~/OpenStack-lab-credentials.sh` too, for conveniense (see README.md)

Go to ~/automation and run it (see README.md)

## OpenStack Lab Project Setup in OVERLAY (OpenStack-in-OpenStack)

After automation is finished, source overlay OpenStack credentials in `/etc/openstack/admin-openrc.sh`

Be nice and prepare some default setup for the candidate.

Provider network:
```
openstack network create --share --external --provider-physical-network provider --provider-network-type flat provider
openstack subnet create --network provider --subnet-range 10.20.30.0/24 --allocation-pool start=10.20.30.100,end=10.20.30.200 --gateway 10.20.30.1 provider
```

Default network:
```
openstack network create lab
openstack subnet create --network lab --subnet-range 172.16.0.0/24 --dns-nameserver 1.1.1.1 lab
```

Default router:
```
openstack router create lab
openstack router set --external-gateway provider lab
openstack router add subnet lab lab
```

Default security group:
```
openstack security group create lab
openstack security group rule create --protocol icmp lab
openstack security group rule create --protocol tcp lab
openstack security group rule create --protocol udp lab
```

Upload a public key that was created before.

Upload Cirros Linux image (http://download.cirros-cloud.net/)

Start at least 3 VMs to check if they can reach each other and the Internet.
Also try pinging them from the workstation. SSH should also work.

## Cleanup

Break something if troubleshooting lab is desired. Update tasks in README.md.

Remove bash history and leave the workstation VM. SSH into it again, clear
bash history again, and you are fine to go.
