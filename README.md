# Ansible Role: Munin

[![Build Status](https://travis-ci.org/geerlingguy/ansible-role-munin.svg?branch=master)](https://travis-ci.org/geerlingguy/ansible-role-munin)

Installs munin, a monitoring system, on RedHat/CentOS.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `vars/main.yml`):

    TODO

## Dependencies

  - geerlingguy.repo-epel

Additionally, if you'd like to view the graphs via HTTP, you will need a server like Apache or Nginx running, to serve the munin-generated HTML and graphs.

## Example Playbook

    - hosts: servers
      roles:
        - { role: geerlingguy.munin }

## License

MIT / BSD

## Author Information

This role was created in 2014 by [Jeff Geerling](http://jeffgeerling.com/), author of [Ansible for DevOps](http://ansiblefordevops.com/).
