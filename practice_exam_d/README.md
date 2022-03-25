
Practice Exam D
To work through this exam, you need a total of five servers that are run-
ning RHEL 8 or CentOS 8. One server needs to be configured as the control
host; the other four servers need to be configured as managed servers, using
the names ansible1.example.com through ansible4.example.com. The IP
addresses used on the managed servers are not important; you can pick anything
that matches your configuration. Make sure the servers meet the following
requirements:
■■ 1 GB of RAM.
■■ A primary disk /dev/sda with a size of 20 GB.
■■ Only on ansible1 and ansible2, a secondary disk /dev/sdb with a size
of 5 GB.
■■ The root user account configured with the password “password” on each
of the servers.
■■ The control server with a user account “ansible.” SSH public and private
keys have been generated for this user. No further configuration has been
done yet.
In the assignments in this exam, you must create scripts and YAML files. Make
sure that all these scripts are stored in the directory /home/ansible unless speci-
fied otherwise.
Common Tasks
1. Configure the control host with a static inventory, as well as the ansible.
cfg configuration file. In the static inventory, configure the following host
groups:
a. Group “test” with ansible1 as a member
b. Group “dev” with ansible2 as a member
c. Group “prod” with ansible3 and ansible4 as members
d. Group “servers” with groups dev and prod as members
M20_Vugt_Exam-D_p002-000.indd 1 18/08/20 1:11 pm
2Red Hat RHCE 8 (EX294) Cert Guide
Ensure that hosts can be reached through their FQDN and also by using the
short name (so ansible1.example.com as well as ansible1).
2. Create a playbook with the name setupreposerver.yml to set up the control
host as a repository host. Make sure this host meets the following require-
ments, which must be done by the playbook:
a. The RHEL 8 installation ISO is loop-mounted on the directory /var/ftp/
repo.
b. The firewalld service is disabled.
c. The vsftpd service is started as well as enabled, and it allows anonymous
user access to the /var/ftp/repo directory.
3. Create a Bash script that configures the managed servers as repository clients
to the repository server that you set up in the previous task. This script must
use ad hoc commands and perform the following tasks:
a. Disable any currently existing repository.
b. Enable access to the BaseOS repository on control.example.com.
c. Enable access to the AppStream repository on control.example.com.
4. Create a Bash script with the name setuphosts.sh that uses ad hoc commands
to complete configuration on the managed servers. This includes
a. Installing Python
b. Creating a user with the name “ansible”
c. Creating a sudo configuration that allows user ansible to run tasks with
root privileges
d. Using an ad hoc command to call the appropriate module to test connec-
tivity to the remote hosts
Exam D Specific Tasks
1. Create playbooks to set up an http server, an http client, and a site playbook to
run these playbooks according to the following requirements:
■■ Configure the inventory file, such that ansible1 is part of the group
webservers and ansible2 is part of the group webclients. (Add this to the
existing inventory file.)
■■ Ensure that the webclient.yml playbook installs the curl package. From
the webserver.yml playbook, you need to install the httpd.conf web server.
M20_Vugt_Exam-D_p002-000.indd 2 18/08/20 1:11 pm
