# Directory Structure, Roles, Ansible Galaxy, RHEL System Roles

Example Project Directory Structure
```shell
project_dir/
    roles/
      role1/
      role2/
        defaults/
          main.yml <-- default vars that may be overwritten
        files/
          file.txt
          file.sh
        meta/
          main.yml <-- role information and dependencies
        vars/
          main.yml <-- role vars not meant to be overwritten
        tasks/
          main.yml <-- role master playbook
        handlers/
          main.yml <-- role handlers
        templates/
          file.conf.j2 <-- jinja2 templates
          
    group_vars/
      group1.yml <-- vars applied to group1
      group2.yml
      all
        vault.yml <-- vars applied to all groups (encrypted with vault)
    host_vars
      host1.yml <-- vars applied to host1
      host2.yml

    ansible.cfg <-- custom ansible.cfg
    inventory <-- custom inventory file
    site.yml <-- master playbook
```
Ansible Galaxy Roles
```shell
ansible-galaxy search <search_term> --author --platforms EL --galaxy-tags
ansible-galaxy info <role.name>
ansible-galaxy install <role.name>,<version>
ansible-galaxy remove <role.name>
ansible-galaxy list
```
```shell
# build custom role
ansible-galaxy init <name>
```
Role Precedence
```shell
    ./roles <-- project roles
    ~/.ansible/roles <-- default location for galaxy installed roles, put custom roles here if used in multiple projects
    /etc/ansible/roles
    /usr/share/ansible/roles
```
Requirements
```shell
requirements.yml

---
- src: geerlingguy.nginx
  name: nginx
  version: 1.1.3
- src: file:///opt/local/roles/myrole.tar
  name: myrole
  version: 1.0.0
```
```shell
# to install roles from requirements.yml
ansible-galaxy install -r requirements.yml -p <install_path>
```
Dependencies
```shell
# role dependencies defined in ./meta/main.yml in same format as requirements
---
dependencies
- src: geerlingguy.nginx
- src: ile:///opt/local/roles/myrole.tar
  name: myrole
  version: 1.0.0

galaxy_info:
...etc...
```
Collections
```shell
# can be defined in same requirements.yml file as roles.
---
roles:
  - src: geerlingguy.nginx
collections:
  - name: ansible.posix
  - name: f5networks.f5_modules
    src: https://cloud.redhat.com/api/automation-hub/
  - name: community.vmware
  - name: ansible.netcommon
    src: https://galaxy.ansible.com
```
```shell
# to install collections from requirements.yml
ansible-galaxy collection install -r requirements.yml
```
