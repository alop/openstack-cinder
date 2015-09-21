Cinder OpenStack Ansible Role
=========

**Status**
* [![Build Status](https://travis-ci.org/openstack-ansible-galaxy/openstack-cinder.svg?branch=master)](https://travis-ci.org/openstack-ansible-galaxy/openstack-cinder) on master branch
* [![Build Status](https://travis-ci.org/openstack-ansible-galaxy/openstack-cinder.svg?branch=development)](https://travis-ci.org/openstack-ansible-galaxy/openstack-cinder) on development branch
* [![Ansible Galaxy](http://img.shields.io/badge/dguerri-openstack--cinder-blue.svg)](https://galaxy.ansible.com/list#/roles/1768) on Ansible Galaxy

OpenStack Cinder image service installation

_Tested on Ubuntu Precise (12.04) and Trusty (14.04)_

Requirements
------------

A DBMS already configured with a user and a database (when applicable).

A RabbitMQ server. See below.

A Keystone server. See below.

For RHEL/CentOS, RHOSP or RDO repositories are needed.

Role Variables
--------------


### Cinder (set by this role)

| Name | Default value | Description |
|---  |---  |---  |
| `cinder_database_url` | `sqlite:////var/lib/cinder/cinder.sqlite` | Database URI |
| `cinder_user` | `cinder` | Admin user for the image service as defined on Keystone |
| `cinder_pass` | `cinder_pass_default` | Password for the image service as defined on Keystone |
| `cinder_bind_host` | `0.0.0.0` | IP address cinder API will bind to |
| `cinder_port` | `8776` | Desired cinder service port |
| `cinder_protocol` | `http` | Desired cinder protocol (http/https) - WiP, do not use. |
| `keystone_admin_port` | `35357` | Keystone admin service port |
| `keystone_hostname` | `localhost` | Hostname/IP address where the keystone service runs |
| `keystone_port` | `5000` | Keystone service port |
| `keystone_protocol` | `http` | Desired cinder protocol (http/https) - WiP, do not use |
| `rabbit_hostname` | `localhost` | Hostname/IP address where the RabbitMQ service runs |
| `rabbit_username` | `rabbit_username_default` | RabbitMQ username for cinder |
| `rabbit_pass` | `rabbit_pass_default` | RabbitMQ password for cinder |
| `cinder_hostname` | `localhost` | Hostname/IP used internally during configuration. localhost is usually ok |
| `cinder_log_dir` | `/var/log/cinder` | Log directory (it must exist) |


Dependencies
------------

None.

Example Playbook
----------------

    - hosts: cinder001
      roles:
        - role: openstack-cinder
          cinder_database_url: "mysql://{{ MYSQL_CINDER_USER }}:{{ MYSQL_CINDER_PASS }}@{{ DATABASE_HOSTNAME }}/{{ MYSQL_CINDER_DB }}"
          cinder_hostname: cinder
          cinder_pass: "{{ CINDER_PASS }}"
          keystone_hostname: keystone
          rabbit_hostname: rabbitmq
          rabbit_username: cinder
          rabbit_pass: "{{ RABBIT_CINDER_PASS }}"

---

A complete Ansible playbook demo, which uses this role, is available on Github (openstack-ansible-galaxy/vagrant-ansible-openstack) <https://github.com/openstack-ansible-galaxy/vagrant-ansible-openstack>

---

Credits
-------
RedHat suport implemented by Abel Lopez < alopgeek@gmail.com >


License
-------

Apache

Author Information
------------------

Copyright (c) 2015 Abel Lopez < alopgeek@gmail.com >
