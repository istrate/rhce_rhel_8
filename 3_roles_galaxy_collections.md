# Directory Structure, Roles, Ansible Galaxy, RHEL System Roles

Project Directory Structure
```shell
- project_dir
  - roles
    - <role1>
    - <role2>
      - defaults
        - main.yml #vars may be overwritten
      - files
      - meta
      - vars
        - main.yml #vars not meant to be overwritten
      - tasks
        - main.yml #starting point
      - handlers
      - templates
  - group_vars
    - <group1>
      - main.yml #vars applied to <group1>
    - all
      - main.yml #vars applied to all groups
  - host_vars
    - <host1>
    - <host2>
      - main.yml #vars applied to <host2>
    - all
  - tasks #tasks not in roles
  - variables
  - files
  - templates
  - ansible.cfg #custom ansible.cfg for project
  - inventory.yml #custom inventory for project
  - site.yml #starting point for execution of project
```
