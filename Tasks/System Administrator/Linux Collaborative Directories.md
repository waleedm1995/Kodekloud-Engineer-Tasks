The Nautilus team doesn't want its data to be accessed by any of the other groups/teams due to security reasons and want their data to be strictly accessed by the devops group of the team.

Setup a collaborative directory /devops/data on Nautilus App 3 server in Stratos Datacenter.

The directory should be group owned by the group devops and the group should own the files inside the directory. The directory should be read/write/execute to the group owners, and others should not have any access.

```
mkdir -p /devops/data
chown -R :devops /devops/data
chmod 770 -R /devops/data
```
