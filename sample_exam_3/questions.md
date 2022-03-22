# Sample Exam 3 Questions for RHCE EX294

## Task 1: Setting up Inventory

- Configure the control host with a static inventory, as well as the ansible.cfg configuration file. In the static inventory, configue the following host groups:
  - Group 'test' with ansible1.example.com as a member
  - Group 'dev' with ansible2.example.com as a member
  - Group 'prod' with ansible3 and ansible4 as members
  - Group 'servers' with groups 'dev' and 'prod' as members
- Ensure that hosts can be reached through their FQDN, but also by using the short name (so ansible1.example.com as well as ansible1)

## Task 2: Setting up a Repository Server

