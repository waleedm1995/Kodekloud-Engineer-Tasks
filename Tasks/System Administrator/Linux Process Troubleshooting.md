The production support team of xFusionCorp Industries has deployed some of the latest monitoring tools to keep an eye on every service, application, etc. running on the systems. One of the monitoring systems reported about Apache service unavailability on one of the app servers in Stratos DC.

Identify the faulty app host and fix the issue. Make sure Apache service is up and running on all app hosts. They might not hosted any code yet on these servers so you need not to worry about if Apache isn't serving any pages or not, just make sure service is up and running. Also, make sure Apache is running on port 8083 on all app servers.


```
# First check from Jump host
telnet stapp01 8083
telnet stapp02 8083
telnet stapp03 8083
# After connecting to identified host
systemctl status httpd -l
netstat | grep 8083
systemctl list-unit-files | grep mail
vi /etc/mail/sendmail.cf               # change port
systemctl restart sendmail
systemctl start httpd

