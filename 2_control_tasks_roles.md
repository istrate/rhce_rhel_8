# Notes on controlling tasks and roles

Adhoc Syntax
```shell
ansible -i <inventory> <group/host> -m <module> -a "<arguments>" -u <user> --ask-pass --check
```
Documentation
```shell
# search for module
ansible-doc -l | grep <search_term>
# show module snippet
ansible-doc -s <module>
# show module use examples (quick method)
ansible-doc <module> | grep EXAMPLES -A 100
# show module use examples (elegant method)
ansible-doc <module> | sed -n '/EXAMPLES/,/RETURN/{/RETURN/!p}'
```
