
Practice Exam C
To work through this exam, you need a total of five servers that are running
RHEL 8 or CentOS 8. One server needs to be configured as the control host;
the other four servers need to be configured as managed servers, using the
names ansible1.example.com through ansible4.example.com. The IP addresses
used on the managed servers are not important; you can pick anything
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
sure that all these scripts are stored in the directory /home/ansible unless
specified otherwise.
Common Tasks
1. Configure the control host with a static inventory, as well as the ansible.
cfg configuration file. In the static inventory, configure the following host
groups:
a. Group “test” with ansible1 as a member
b. Group “dev” with ansible2 as a member
c. Group “prod” with ansible3 and ansible4 as members
d. Group “servers” with groups dev and prod as members
Ensure that hosts can be reached through their FQDN and also by using
the short name (so ansible1.example.com as well as ansible1).
M19_Vugt_Exam-C_p002-000.indd 1 18/08/20 1:11 pm
2Red Hat RHCE 8 (EX294) Cert Guide
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
c. Creating a sudo configuration that enables user ansible to run tasks with
root privileges
d. Using an ad hoc command to call the appropriate module to test connec-
tivity to the remote hosts
Exam C Specific Tasks
1. Write a playbook that detects storage devices and writes a report with device
names to the file /tmp/devices.txt. This file should meet the following
requirements:
a. Support must be offered for a diversity of storage device names, such as
/dev/sda and /dev/vda.
b. For each host, the file should have the line “primary device DEVICENAME
found on HOSTNAME,” where DEVICENAME is replaced with the actual
name of the device and HOSTNAME is replaced with the actual name of
the host.
c. If a second disk device is found, the file should have the line “second device
DEVICENAME found on HOSTNAME.”
d. If no second disk device is found, the file should have the line “no second
device found on HOSTNAME.”
M19_Vugt_Exam-C_p002-000.indd 2 18/08/20 1:11 pm
3Practice Exam C
2. Write a playbook that sets up storage and meets the following requirements:
a. If a second disk is found, a volume group with the name vgfiles should be
created. This volume group may use all available disk space.
b. If no second disk is found, the playbook should print the line “no work to
do” and fail further task execution on this host.
c. An LVM logical volume with the name lvfiles and a size of 1 GB should be
created.
d. The LVM logical volume should be formatted with an XFS file system.
e. The LVM logical volume should be persistently mounted on the directory
/lvfiles.
3. Write a playbook that generates a file with the name /tmp/hosts, based on dis-
covered inventory information. The file must have the same format as the /etc/
hosts file.
4. Write a requirements file that installs the nginx role and the docker role
created by geerlingguy and is available on galaxy.ansible.com.
5. Write a playbook that installs, starts, and enables the httpd service. Ensure the
httpd service is listening on port 88 and is accessible through the firewall. In
the same playbook, write a play that tests access to the service and prints an
error message if the service could not be accessed.
6. Write a playbook that uses the RHEL system role to synchronize time on
all managed servers. Ensure that time is synchronized with the pool.ntp.org
servers.
M19_Vugt_Exam-C_p002-000.indd 3 18/08/20 1:11 pm
