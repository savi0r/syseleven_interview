# An Ansible role to pick an image from OpenStack cloud

This role finds an image in OpenStack cloud, according to specified constains.

# How to use

Configure desired constains in `openstack_image_constrains` list. All of these
must match, in order for image to enter resulting image list. After the role is
executed, all images that match these constrains will be available in
`openstack_selected_images` list.

For example, to get list of Ubuntu Bionic images:

```
openstack_image_constrains:
  - field: os_distro
    operation: match
    value: ubuntu
  - field: os_version
    operation: match
    value: '18.04'
```

`field`, `operation` and `value` will be used in selectattr() jinja2 filter like this:
```
selectattr(field, operation, value)
```

Resulting list will be sorted by image upload date, descending. That means that
in theory, first image in the list will be latest.

You can use resulting image list to provision instance like this:

```
- name: Create a new instance
  os_server:
       state: present
       name: vm1
       key_name: ansible_key
       flavor: 4
       image: "{{ openstack_selected_images[0].id }}"
```

