Role Name
=========

Installs and configures Zabbix agent monitoring (https://www.zabbix.com)  
Define version to install by setting zabbix_version: x.x (2.2|2.4|3.0)

Requirements
------------

None

Role Variables
--------------

````
---
# defaults file for ansible-zabbix-agent
pri_domain_name: example.org
zabbix_agent_advanced_parameters: ''  #define add'l advanced parameters
#  - name:
#    value:
zabbix_agent_enable_remote_commands: false  #Whether remote commands from Zabbix server are allowed
zabbix_agent_group: all  #define Ansible inventory that zabbix agents are members of
zabbix_agent_include:  #You may include individual files or all files in a directory in the configuration file
  - '/etc/zabbix/zabbix_agentd.d/'
#  - '/usr/local/etc/zabbix_agentd.userparams.conf'
#  - '/usr/local/etc/zabbix_agentd.conf.d/'
#  - '/usr/local/etc/zabbix_agentd.conf.d/*.conf'
zabbix_agent_listen_ip: 0.0.0.0  #IP addresses that the agent should listen on
zabbix_agent_listen_port: 10050  #Agent will listen on this port for connections from the server
zabbix_agent_logfile: '/var/log/zabbix/zabbix_agentd.log'
zabbix_agent_logfile_size: 0  #defines Maximum size of log file in MB (0-1024) 0=disable
zabbix_agent_log_remote_commands: false  #Enable logging of executed shell commands as warnings
zabbix_agent_server_active:  #Zabbix servers for active checks
  - '127.0.0.1'
  - 'node0.{{ pri_domain_name }}'
zabbix_agent_servers:
  - 'node0.{{ pri_domain_name }}'
zabbix_agent_start_agents: 3  #Number of pre-forked instances of zabbix_agentd that process passive checks
zabbix_debian_repo_info:  #defines Debian based package repo info
  package: 'zabbix-release_{{ zabbix_version }}-1+{{ ansible_distribution_release|lower }}_all.deb'
  url: 'http://repo.zabbix.com/zabbix/{{ zabbix_version }}/{{ ansible_distribution|lower }}/pool/main/z/zabbix-release'
zabbix_server: 'node0.{{ pri_domain_name }}'  #define zabbix server for agents
zabbix_version: 3.0
````

Dependencies
------------

None

Example Playbook
----------------

````
- hosts: all
  become: true
  vars:
    - pri_domain_name: 'test.vagrant.local'
  roles:
    - role: ansible-zabbix-agent
  tasks:
````

License
-------

BSD

Author Information
------------------

Larry Smith Jr.
- @mrlesmithjr
- http://everythingshouldbevirtual.com
- mrlesmithjr [at] gmail.com
