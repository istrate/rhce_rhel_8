# Notes on controlling tasks and roles

Adhoc Syntax
```shell
ansible -i <inventory> <group/host> -m <module> -a "<arguments>" -u <user> --ask-pass --check
```
Documentation
```shell
# search list of modules
ansible-doc -l | grep <search_term>
# show module snippet
ansible-doc -s <module>
# show module use examples (quick - show 100 lines)
ansible-doc <module> | grep EXAMPLES -A 100
# show module use examples (elegant - show all examples)
ansible-doc <module> | sed -n '/EXAMPLES/,/RETURN/{/RETURN/!p}'
```
Ansible Vault
```shell
# command line switches
--ask-vault-pass 
--vault-password-file=<path>

# vault password file variable
# ensure file is protected ie. chmod 600
vault-password-file: <path>
```
Custom Local Facts (on managed node)
```shell
/etc/ansible/facts.d/<name>.fact

[fact_name]
var1: value
var2: value
...etc...
```
```shell
# addressing a local fact variable
ansible_local.<name>.<fact_name>.var1
```
Error Handling
```shell
ignore_errors: yes
force_handlers: yes
failed_when: <conditional>
```
```shell
# fail module example
- name: print error message
  fail:
    msg: the task failed because.....
  when: "'condition' in registered_var.err"
```
```shell
# using blocks
block:
rescue:
always:
```
