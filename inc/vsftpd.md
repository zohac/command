# Vsftpd
## Install (Ubuntu)
First you need vsftp and PAM installed
```bash
apt-get install vsftpd libpam-pwdfile
```

## Configuration
Edit /etc/vsftpd.conf
```bash
nano /etc/vsftpd.conf
```
then paste in the following

```text
listen=YES
anonymous_enable=NO
local_enable=YES
write_enable=YES
local_umask=022
local_root=/var/www
chroot_local_user=YES
allow_writeable_chroot=YES
hide_ids=YES

#virutal user settings
user_config_dir=/etc/vsftpd_user_conf
guest_enable=YES
virtual_use_local_privs=YES
pam_service_name=vsftpd
nopriv_user=vsftpd
guest_username=vsftpd
```
Edit to your exact needs the most important bit for virtual users is everything after the virtual user settings comment

## Creating User
You can either use a database or htpasswd I found htpasswd faster and easier to use.
make a directory to store your users
```bash
mkdir /etc/vsftpd
htpasswd -cd /etc/vsftpd/ftpd.passwd user1
```
adding additional users just omit the -c
```bash
htpasswd -d /etc/vsftpd/ftpd.passwd user2
```
Once your users are created you can now change your PAM config file
```bash
nano /etc/pam.d/vsftpd
```
and remove everything inside this file and replace with the following
```text
auth required pam_pwdfile.so pwdfile /etc/vsftpd/ftpd.passwd
account required pam_permit.so
```
This will enable login for your virtual users defined in /etc/vsftpd/ftpd.passwd and will disable local users

Next we need to add a user for these virtual users to use. These users will not have access to the shell and will be called vsftpd
```bash
useradd --home /home/vsftpd --gid nogroup -m --shell /bin/false vsftpd
```
the user must match guest_username=vsftpd in the vsftpd conf file

Defining Directory Access

The important line here is the following
```text
user_config_dir=/etc/vsftpd_user_conf
```
this means that when user1 logs in it will look for the following file

/etc/vsftpd_user_conf/user1

this file the same as the vsftpd.conf so you can define a new local_root

going back to the question we want user1 to only have access to var/www/website_name1/sub_folder1, so we need to create the vsftpd_user_conf folder:
```bash
mkdir /etc/vsftpd_user_conf
```
Now create the user file:
```bash
nano /etc/vsftpd_user_conf/user1
```
and enter the following line
```text
local_root=/var/www/website_name1/sub_folder1
```
Now restart vsftp
```bash
service vsftpd restart
```
you should now be able to login as user1 who will only be able to see var/www/website_name1/sub_folder1 and any folder and file inside it.

That's it you can now add as many users as you want and limit their access to whatever folder you wish.

important to remember if you do not create a user conf file it will default to the var/www folder as root (in the example above)

If the subfolder is intended to be modifiable by the user, it might be necesary to change the owner of the shared subfolder:
```bash
chown vsftpd:nogroup /var/www/website_name1/sub_folder1
```

## Source
* [Ubuntu - serveur ftp](https://guide.ubuntu-fr.org/server/ftp-server.html)
* [Configuration - 1](https://www.digitalocean.com/community/tutorials/how-to-set-up-vsftpd-on-centos-6--2)
* [Configuration - 2](https://doc.fedora-fr.org/wiki/Vsftpd_:_Installation_et_configuration)
* [Configuration - 3](https://doc.ubuntu-fr.org/tutoriel/vsftpd_multi-utilisateurs_multi-dossiers_avec_db_ou_mysql)
* [Configuration - 4](https://askubuntu.com/questions/575523/how-to-setup-virtual-users-for-vsftpd-with-access-to-a-specific-sub-directory)
* [Configuration - ssl](https://hostadvice.com/how-to/how-to-install-and-configure-vsftpd-on-ubuntu-18-04/)
* [user](https://serverfault.com/questions/544850/create-new-vsftpd-user-and-lock-to-specify-home-login-directory)
