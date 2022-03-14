# Managing Software and Users

### Managing Software
Useful software to install on control node:
dnf-utils
createrepo
vsftpd

Userful modules for managing packages:
package/yum/dnf:
yum_repository:
package_facts:
rpm_key
redhat_subscription:
rhn_register:
rhn_channel:

### Managing Users
Useful modules for managing users:
user:
group:
pamd:
openssh_keypair:
authorized_key:
lineinfile

Create Encrypted Password
```shell
ansible localhost -m debug -a "msg={{ 'password' | password_hash('sha512', 'mysecretsalt') }}
```
Example using authorized_key module
```yaml
tasks:
- name: distribute public key
  authorized_key:
    user: "{{ user }}"
    key: "{{ lookup( 'file', '/home/' + {{ user }} + '/.ssh/id_rsa.pub' ) }}"
```
Example Jinja2 Template for sudoers config
```yaml
# variables defining groups to be created on managed node
sudo_groups:
  - name: devs
    sudo: false
  - name: admins
    sudo: true
  - name: dbas
    sudo: false
```
```ini
# jinja2 control template incorporating if statement embedded in for loop
{% for item in sudo_groups %}
{% if item.sudo %}

%{{item.name}} ALL=(ALL) NOPASSWD: ALL

{% endif %}
{% endfor %}
```
