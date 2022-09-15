# Ansible role for OpenStack Instance Provisioning

This role will not only boot an instance in OpenStack cloud, but also:
* Install Python so Ansible can properly work
* Optionally update operating system and apply all security patches
* Reboot freshly built instance if it is required after the update, and wait for it to come back

This role will also update ansible host dynamically, it means that you may run any other roles after this one,
and they will be correctly executed on the host which was not there initially.

The catch is, gather_facts needs to be disabled, since Ansible will try to connect to host which does not yet exists.

This is how your playbook should like:

```
---

# Instance provisioning
- hosts: my_hosts_in_openstack
  gather_facts: False
  become: False
  roles:
    - openstack-select-image
    - openstack-instance

# Instance configuration
- hosts: my_hosts_in_openstack
  gather_facts: True
  become: True
  roles:
    - role1
    - role2
    - role3
```

Have a look at [openstack-select-image](https://github.com/rnurgaliyev/ansible-openstack-select-image) role as well.

## How to use

This role has following variables defined, all of them are pretty self explanatory.
```
# These values have to be overriden
openstack_instance_flavor: ""
openstack_instance_image: ""
openstack_instance_key_name: ""
openstack_instance_network: ""
openstack_instance_security_groups: []

# Set region if required
#openstack_instance_region_name: ""

# These vaules can be overriden if required
openstack_instance_default_user: "ubuntu"
openstack_instance_gather_facts: True
openstack_instance_install_python: True
openstack_instance_name: "{{ inventory_hostname }}"
openstack_instance_perform_full_upgrade: True
openstack_instance_public_ip: False
```
