Ansible Role: Docker Swarm
==========================

![CI](https://github.com/fgierlinger/ansible-role-docker-swarm/workflows/CI/badge.svg?branch=master)

An ansible role that configures a docker swarm.

Requirements
------------

* `docker` installed on all hosts
* `python-docker` installed on all hosts
* `python-six` when using debian 10 or ubuntu 18.04

Both requirements can be satisfied as follows:

    - hosts: all
      roles:
        - role: geerlingguy.docker
        - role: geerlingguy.pip
          vars:
            pip_install_packages:
              - name: docker

Role Variables
--------------

Available variables are listed below, along with default values.

    docker_swarm_network_interface: eth0
    docker_swarm_port: 2377
    docker_swarm_manager: false

The first host of the inventory is always used as master node. If another host
should be used to form the cluster, set `docker_swarm_primary_master_name` to
the inventory name of one of the hosts. 

WARNING! The first host is ALWAYS configured as master, nontheless the value of
`docker_swarm_manager` for the first host.

All other hosts will join the cluster as worker nodes. Set
`docker_swarm_manager` to true for each host that should be confiugred as
manager.If you wish to exclude a host out of the docker swarm, make sure the
scope of the play is limited to those hosts.

    # playbook.yml example
    ---
    - hosts: swarmMembers
      roles:
        - role: fgierlinger.docker_swarm

Usage
-----

Include the role in your playbook. All the hosts will become part of the docker
swarm cluster. The first host defined in the inventory wll be used to join the
other hosts.

Example Playbook
----------------

    - hosts: all
      roles:
         - role: fgierlinger.docker_swarm

License
-------

MIT

Author Information
------------------

Frédéric Gierlinger
