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

