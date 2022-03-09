# Set Up Managed Environment

## On Control Node
Create ansible user and install Python
```shell
useradd ansible
echo "password" | passwd --stdin ansible
echo -e "ansible\tALL=(ALL)\tNOPASSWD: ALL" > /etc/sudoers.d/ansible
yum install -y python3 python3-pip
alternatives --set python /usr/bin/python3
su - ansible
```
Install Ansible
```shell
# ansible install with pip
pip3 install ansible --user
```
```shell
# ansible install with subscription-manager
subscription-manager repos --list
subscription-manager repos --enable ansible-2.9-for-rhel-8-x86_64-rpms
yum install -y ansible
```

> now configure /etc/hosts for name resolution of managed nodes

Configure tab spacing for yaml on vim (optional)
```shell
touch ~/.vimrc
echo "autocmd FileType yaml setlocal ai ts=2 sw=2 et" > ~/.vimrc
```
Customize ansible.cfg
```shell
~/.ansible.cfg

[defaults]
inventory = ~/inventory
remote_user = ansible
host_key_checking = false
deprecation_warnings = false

[privilege escalation]
become = true
become_user = root
become_method = sudo
become_ask_pass = false
```
Customize default inventory
```shell
~/inventory
    
[nodes]
node1.example.com
node2.example.com
node3.example.com
```
```shell
# verify default inventory is working
ansible all --list-hosts
```
Write playbook to set up managed nodes
```shell
~/setup_managed_nodes.yml

---
- name: setup managed nodes
  hosts: all
  gather_facts: no
  tasks:
  - raw: |
      useradd ansible;
      touch /etc/sudoers.d/ansible;
      echo -e "ansible\tALL=(ALL)\tNOPASSWD: ALL" > /etc/sudoers.d/ansible;
      yum install -y python3;
      alternatives --set python /usr/bin/python3
```
Run playbook
```shell
ansible-playbook --user=root --ask-pass setup_managed_nodes.yml
```
Generate and copy SSH key to managed nodes
```shell
su - ansible
ssh-keygen
### do not use a passphrase ###
ssh-copy-id node1
...etc...
```
Run adhoc ping test
```shell
ansible all -m ping
```
