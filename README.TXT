
To apply all playbooks currently assigned to site:
--------------------------------------------------

  ansible-playbook site.yml


To only run a particular playbook, example setup services hosts:
----------------------------------------------------------------

  ansible-playbook services.yml
           or
  ansible-playbook site.yml -l services
           or
  ansible-playbook site.yml -l my_extra_hosts


Hosts are described in the 'hosts' file:
----------------------------------------

  Example:

  [my_extra_hosts]
  10.10.10.1
  10.10.10.2
  ...


Roles are implemented to be independent entities to be included by playbooks:
-----------------------------------------------------------------------------

├── roles
│   ├── base_config
│   │   ├── tasks
│   │   │   └── main.yml
│   │   └── vars
│   │       └── main.yml
│   ├── docker_ce
│   │   ├── tasks
│   │   │   └── main.yml
│   │   └── vars
│   │       └── main.yml
│   ├── epel-repo
│   │   ├── tasks
│   │   │   └── main.yml
│   │   └── vars
│   │       └── main.yml
│   └── etcd_cluster
│       ├── tasks
│       │   └── main.yml
│       ├── templates
│       │   └── etcd.service.j2
│       └── vars
│           └── main.yml


Example setup of ~/.ssh/config
------------------------------

host hdc-bastion
    hostname 128.224.253.178
    user centos
    IdentityFile ~/.ssh/hdcsaas.pem
    ServerAliveInterval 60
    ForwardAgent yes
    TCPKeepAlive yes
    StrictHostKeyChecking no
    CheckHostIP no
    GSSAPIAuthentication no

host hdc-vm-1
    hostname 10.10.20.3
    user centos
    IdentityFile ~/.ssh/hdcsaas.pem
    ProxyCommand ssh -q hdc-bastion -W %h:%p
    StrictHostKeyChecking no
    ServerAliveInterval 60
    CheckHostIP no
    GSSAPIAuthentication no

host hdc-vm-2
    hostname 10.10.20.11
    user centos
    IdentityFile ~/.ssh/hdcsaas.pem
    ProxyCommand ssh -q hdc-bastion -W %h:%p
    StrictHostKeyChecking no
    ServerAliveInterval 60
    CheckHostIP no
    GSSAPIAuthentication no

host hdc-vm-3
    hostname 10.10.20.8
    user centos
    IdentityFile ~/.ssh/hdcsaas.pem
    ProxyCommand ssh -q hdc-bastion -W %h:%p
    StrictHostKeyChecking no
    ServerAliveInterval 60
    CheckHostIP no
    GSSAPIAuthentication no

