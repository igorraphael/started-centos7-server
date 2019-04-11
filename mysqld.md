#### Start  with cent
First enter the root server and run update.
```sh
$ yum update
```
Check SELinux status
```sh
$ sestatus
SELinux status:                enabled
SELinuxfs mount:               /sys/fs/selinux
SELinux root directory         /etc/selinux
Loaded policy name:            targeted
Current mode:                  enforcing
Mode from config file:         enforcing
Policy MLS status:             enable
Policy deny_unknown status     allowed
Max kernel policy version      31
$
```
#### Install Mysql
Before install run update your system.
```sh
$ yum update
```
You will need wget
```sh
$ yum install wget
```
```sh
$ wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm
$ rpm -ivh mysql-community-release-el7-5.noarch.rpm
$ yum update
```
Install mysql, start service and enable startup.
```sh
$ yum install mysql-server
$ yum systemctl start mysqld
$ yum systemctl enable mysqld
```
#### Alter port 3306 default Mysql
In order to change the default MySQL/MariaDB database port in Linux, open MySQL server configuration file for editing
```sh
$ vi /etc/my.cnf.d
[mysqld]
port = 1996
```
*Open the file with your editor, and add the line port = 1996 (at the study level, enter your date of birth).*

Check what port mysql is running on.
```sh
$ semanage port -l | grep mysql
-bash: semanage: command not found
```
*semanage is used to configure certain parts of SELinux policy without requiring modification to or recompilation from policy sources. To use install policycoreutils-python*
```sh
$ yum -y install policycoreutils-python
```
Now search for the mysqld_port_t rule
```sh
$ semanage port -l | grep mysqld_port_t
mysqld_port_t        tcp    1186,3306, 63132-63164
```
Next, add the below SELinux rule to bind MySQL socket on the new port and restart the database daemon to apply changes, by issuing the following commands.
```sh
$ semanage port -a -t no mysqld_port_t -p tcp 1996
$ systemctl restart mysqld
$ semanage port -l | grep mysqld_port_t
mysqld_port_t tcp    1996,1186,3306, 63132-63164
```