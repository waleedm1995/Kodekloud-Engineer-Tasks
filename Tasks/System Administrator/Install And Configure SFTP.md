Some of the developers from Nautilus project team have asked for SFTP access to at least one of the app server in Stratos DC. After going through the requirements, the system admins team has decided to configure the SFTP server on App Server 2 server in Stratos Datacenter. Please configure it as per the following instructions:

a. Create an SFTP user mariyam and set its password to dCV3szSGNA.

b. Password authentication should be enabled for this user.

c. Set its ChrootDirectory to /var/www/webdata.

d. SFTP user should only be allowed to make SFTP connections.

```
useradd mariyam
passwd mariyam
mkdir -p /var/www/webdata
ll /var/www/webdata
chown root:root /var/www
chmod -R 755 /var/www
vi /etc/ssh/sshd_config 

#Subsystem      sftp    /usr/libexec/openssh/sftp-server
Subsystem       sftp    internal-sftp
Match User mariyam
ForceCommand internal-sftp
PasswordAuthentication yes
ChrootDirectory /var/www/webdata
PermitTunnel no
AllowTcpForwarding no
X11Forwarding no
AllowAgentForwarding no
# Example of overriding settings on a per-user basis

systemctl restart sshd
systemctl status sshd
sftp mariyam@localhost
```
