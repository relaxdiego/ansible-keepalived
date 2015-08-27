Keepalived
=========

This role installs keepalived and configures it according to the variables you'll pass to the role.

Requirements
------------

No fancy requirements. Only package and file management in the role.

Role Variables
--------------

By default, this role doesn't configure keepalived, it barely installs it. This way keepalived is fully flexible based on what you give as input.
Examples are given in the vars folder. Don't try them immediately, they won't work! (You need to define VIPs, passwords, etc.). The examples are only a source of inspiration.

The main variables are:

* keepalived_instances: This is a mandatory dict. It gathers information about the vips, the prefered state (master/backup), the VRRIP IDs and priorities, the password used for authentication...
* keepalived_sync_groups: This is a mandatory dict. It groups items defined in keepalived_instances, and (if desired) allow the configuration of notifications scripts per group of keepalived_instances. Notification scripts are triggered on keepalived's state change and are facultative.
* keepalived_scripts: This is an optional dict where you could have checking scripts that can trigger the notifications scripts.

Please check the examples for more explanations on how these dicts must be configured.

An example of a notification script is also given, in the files folder.

Dependencies
------------

No dependency

Example Playbook
----------------

Here is how you could use the role

    - hosts: keepalived_servers[0]
      vars_files:
        - roles/keepalived/vars/keepalived_haproxy_master_example.yml
      roles:
         - keepalived
    - hosts: keepalived_hosts:!keepalived_hosts[0]
      vars_files:
        - roles/keepalived/vars/keepalived_haproxy_backup_example.yml
      roles:
         - keepalived

License
-------

Apache2

Author Information
------------------

Jean-Philippe Evrard
