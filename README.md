Role Name
=========

This role install and configure a openstack nova compute node. This role allows  make a all-in installation,
so that, it installs the compute node in a machine with an openstack controller installation (installing LIP-Computing.os-controller).

Requirements
------------

This role installs authomatically the openstack centos packages:
 - centos-release-liberty
 - centos-release-qemu-ev
 - centos-release-ovirt36

Role Variables
--------------

* openstack_all_in: It indicates installation all-in (controller and compute node in same host). If true it will make a minimal installation, because the host
has already installed most of the packages.
* openstack_version: "liberty" version is supported
* openstack_controller_host: controller hostname
* openstack_compute_node_host: compute node hostname
* openstack_cidr: openstack internal network CIDR
* openstack_compute_node_ip: controller ip
* openstack_controller_ip: compute node ip (can be the same as controller in all-in installation)

* openstack_rabbit_host: rabbit host name
* openstack_rabbit_user: rabbit username
* openstack_rabbit_pass: rabbit password

* openstack_admin_vip: administration host (could be openstack_controller_host in in all-in installation)
* openstack_os_identity_api_version: openstack identification api version
* openstack_ath_uri: public openstack authentication uri
* openstack_ath_url: internal openstack authentication url

* openstack_nova_keystone_password: keystone password for nova user.
* openstack_neutron_keystone_password: keystone password for neutron user
* openstack_keystone_auth_region: authentication region (RegionOne)

* openstack_neutron_bridge_interface: openvswitch external bridge (br-ex)


Example Playbook
----------------
This is an example of all-in installation. We install the compute node in a machine with openstack controller installed.
    - hosts: localhost
      var:
       openstack_version: "liberty"
       openstack_controller_host: localhost
       openstack_compute_node_ip: 127.0.0.1
       openstack_controller_ip: 127.0.0.1
       penstack_cidr: 127.0.0.0/8
       openstack_all_in: True
      roles:
        - LIP-Computing.nova-compute-node

License
-------

Apache 2.0

Author Information
------------------

Contact: jorgesece@lip.pt
