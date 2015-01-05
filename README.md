# ansible-role-nsd [![Build Status](https://travis-ci.org/elnappo/ansible-role-nsd.svg?branch=master)](https://travis-ci.org/elnappo/ansible-role-nsd)

Installs and start nsd on boot. Get more informations about nsd at [https://www.nlnetlabs.nl/projects/nsd/]()
## Requirements
Ubuntu or Debian

## Role Variables
* `nsd_setup_ufw: true` : Add a ufw rule to allow port `nsd_port`
* `nsd_server_count: 1`
* `nsd_do_ip4: "yes"`
* `nsd_do_ip6: "yes"`
* `nsd_port: 53`
* `nsd_hide_version: "yes"`
* `nsd_remote_control_enable: "no"`
* `nsd_remote_control_port: 8952`
* `nsd_remote_control_interfaces: [127.0.0.1, ::1]`

## Dependencies
None.

## Example Playbook
    - hosts: ns1.example.com
	  remote_user: root
	  vars:
	    ns1_zones:
	      - name: example.com
	        secret: hMUg6ohC7jV01jhL3HYITXD8T5U7pxvUai5TrOb+BPo=
	        slaves:
	         - 10.0.0.2
	         - 10.0.0.3
	      - name: example.io
	        secret: Z+zGmmEOdOzyAZR2xUgld9WL2XwVFVWw6tYBmd9escU=
	        masters: [10.0.0.1, 10.0.1.1]
	      - name: example.net
	        masters: [10.0.0.1]
	        slaves:
	         - 10.0.0.2
	         - 10.0.0.3
	      - name: example.org
	  
	  roles:
	    - { role: elnappoo.ansible-role-nsd, zones: "{{ slave_zones }}"}

## License
MIT

## Author Information
elnappo <elnappoo@gmail.com>
