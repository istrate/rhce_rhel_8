# Inventories and Troubleshooting
##
Can have multiple inventory files in a directory as the source
```shell
~/ansible.cfg
inventory = ~/inventory/

~/inventory/
  /webservers.yml
  /fileservers.yml
```
Exmaple Inventory
```shell
# yaml format
---
nodes:
  hosts:
    node1.example.com:
      ansible_host: 10.0.0.164
    node2.example.com:
      ansible_host: 10.0.0.166
    node3.example.com:
      ansible_host: 10.0.0.167
```
```shell
# ini format
[nodes]
node1.example.com ansible_host=10.0.0.164
node2.example.com ansible_host=10.0.0.166
node3.example.com ansible_host=10.0.0.167
```
> NB. View an inventory in json format: ansible-inventory --list

####Hosts wildcard syntax:
- hosts: '*.example.com'  <- any hosts ending example.com
- hosts: '192.168.*'  <- any hosts with ip beginning 192.168
- hosts: 'web*'  <- any hosts with hostname beginning with web
- hosts: web1,db1,192.168.4.2  <- comma separated list of hosts
- hosts: web,&eastcoast  <- members of group web & eastcoast
- hosts: web,!web1  <- members of group web but not web1
- hosts: all,!web  <- all hosts but not members of group web

####Parallelism
```shell
# in ansible.cfg (default is 5 but can be much higher)
forks = n

# from command line
-f n
```
```shell
# other examples of useful statements/arguments
serial: 3        <- set batch size number or percentage of hosts
throttle: 1      <- restrict number of workers, must be lower than forks value
order: sorted    <- determin order in which hosts are processed (sorted,reverse_sorted,shuffle,reverse_inventory)
run_once: true   <- only run task against first host or use in conjuction with delegate_to:
```
