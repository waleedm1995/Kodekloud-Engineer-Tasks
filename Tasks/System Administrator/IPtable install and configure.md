We have one of our websites up and running on our Nautilus infrastructure in Stratos DC. Our security team has raised a concern that right now Apache’s port i.e 8088 is open for all since there is no firewall installed on these hosts. So we have decided to add some security layer for these hosts and after discussions and recommendations we have come up with the following requirements:



Install iptables and all its dependencies on each app host.

Block incoming port 8088 on all apps for everyone except for LBR host.

Make sure the rules remain, even after system reboot.

```
yum install iptables-services -y
systemctl start iptables
iptables -I INPUT -p tcp --dport 8088 -j DROP
iptables -I INPUT -p tcp -s 172.16.238.14 --dport 8088 -j ACCEPT
iptables -L --line-numbers
service iptables save             # to make persistent across reboots
```
