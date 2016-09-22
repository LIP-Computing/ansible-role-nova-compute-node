Role Name
=========

This role installs and configures a openstack nova compute node.
This role allows to make a all-in installation, so that, it installs the compute node in a host which has
already installed an openstack controller (installing LIP-Computing.os-controller).

Requirements
------------

* Disable SELinux (reboot is required).
* Ensure the system has configured swap memory

Role Variables
--------------

    openstack_all_in: True or False, indicates all-in installation (*) 
    s.
    openstack_version: "liberty" version is supported
    openstack_controller_host: controller hostname
    openstack_compute_node_host: compute node hostname
    openstack_cidr: openstack internal network CIDR
    openstack_compute_node_ip: controller ip
    openstack_controller_ip: compute node ip (can be the same as controller in all-in installation)
    
    #Rabbitmq variables
    openstack_rabbit_host: rabbit_host ("{{ openstack_controller_host }}" by default)
    openstack_rabbit_user: rabbit_user (openstack by default)
    openstack_rabbit_pass: rabbit password ("{{ openstack_admin_password }}" by default)
    
    openstack_admin_vip: administration IP ("{{ openstack_controller_host }}" by default)
    openstack_os_identity_api_version: identity api version (3 by default)
    openstack_ath_uri: auth_uri, authorization uri ("http://{{ openstack_admin_vip }}:5000" by default)
    openstack_ath_url: auth_url, authorization url ("http://{{ openstack_admin_vip }}:35357" by default)
    
    openstack_nova_keystone_password: nova keystone password ("{{ openstack_admin_password }}" by default)
    openstack_neutron_keystone_password: neutron keystone password ("{{ openstack_admin_password }}" by default)    
    openstack_keystone_auth_region: region_name (RegionOne by default)
    
    openstack_neutron_bridge_interface: external bridge of openvswitch ("br-ex" by default)

(*) The openstack-all-in variable indicates installation all-in (controller and compute node in same host). 
If true it will make a minimal installation, because the host already should have most of the required packages.

Playbook Examples
----------------
This is an example of all-in installation. We install the compute node in a machine with openstack controller installed.

    # compute_playbook.yml
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

Execute
------------

The ansible roles are executed by the command:
ansible-playbook <-i host_list> compute_playbook.yml 

License
-------

Apache 2.0

Author Information
------------------

Contact: jorgesece@lip.pt
