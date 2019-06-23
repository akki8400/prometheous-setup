# prometheous-setup
This repo is for complete setup of prometheous

This repository setups the complete stack of prometheus.
Setups :

Prometheus
ALertmanager
Node Exporter
Cadvisor


All config varibbles are defined at:

```
var/main.yml
```

Modifiy all variables according to requirement.

This repo contains the 4 roles each setups mentioned above.

Role wise templates are in particular roles tamplate dir.

To add more alert roles
```
roles/prometheus/template/alert-rules.j2
```

cadvisor is running over docker container.
It is assumed dockers is preinstalled, up and running on the required servers.
Add hosts in file mentioned below according to host group.
```
hosts
```

Playbook

```
Cadvisor installation
- hosts: cadvisor
  vars_files:
    - vars/main.yml
  roles:
    - cadvisor

#node_exporter installation
- hosts: node_exporter
  vars_files:
    - vars/main.yml
  roles:
    - node-exporter

#alertmanager installation
- hosts: alertmanager
  vars_files:
    - vars/main.yml
  roles:
    - alertmanager

#prometheus installation
- hosts: prometheus
  become: yes
  vars_files:
    - vars/main.yml
  roles:
    - prometheus
```
