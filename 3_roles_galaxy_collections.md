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
          foo.sh
        meta/
          main.yml <-- role information and dependencies
        vars/
          main.yml <-- role vars not meant to be overwritten
        tasks/
          main.yml <-- role master playbook
        handlers/
          main.yml <-- role handlers
        templates/
          httpd.conf.j2 <-- jinja2 templates
          smb.conf.j2
          
    group_vars/
      group1.yml <-- vars applied to group1
      group2.yml
      all
        vault.yml <-- vars applied to all groups
    host_vars
      host1.yml <-- vars applied to host1
      host2.yml

    ansible.cfg <-- custom ansible.cfg
    inventory <-- custom inventory file
    site.yml <-- master playbook
```
