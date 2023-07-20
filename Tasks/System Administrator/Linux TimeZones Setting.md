During the daily standup, it was pointed out that the timezone across Nautilus Application Servers in Stratos Datacenter doesn't match with that of the local datacenter's timezone, which is Pacific/Bougainville.

Correct the mismatch.

```
timedatectl
ls -l /etc/localtime
timedatectl list-timezones
timedatectl set-timezone Pacific/Bougainville
```
        or
```
sudo rm -rf /etc/localtime
sudo ln -s /usr/share/zoneinfo/Pacific/Bougainville /etc/localtime
date
```
