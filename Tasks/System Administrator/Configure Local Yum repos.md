The Nautilus production support team and security team had a meeting last month in which they decided to use local yum repositories for maintaing packages needed for their servers. For now they have decided to configure a local yum repo on Nautilus Backup Server. This is one of the pending items from last month, so please configure a local yum repository on Nautilus Backup Server as per details given below.

a. We have some packages already present at location /packages/downloaded_rpms/ on Nautilus Backup Server.

b. Create a yum repo named local_yum and make sure to set Repository ID to local_yum. Configure it to use package's location /packages/downloaded_rpms/.

c. Install package samba from this newly created repo.

```
yum repolist
vi /etc/yum.repos.d/local_yum.repo
[local_yum]
name=local_yum
baseurl=file:///packages/downloaded_rpms/
enabled = 1
gpgcheck = 0
yum repolist
yum clean all
yum install --disablerepo="*" --enablerepo="local_yum" samba
yum list samba
```
