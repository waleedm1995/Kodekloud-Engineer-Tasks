xFusionCorp Industries has planned to set up a common email server in Stork DC. After several meetings and recommendations they have decided to use postfix as their mail transfer agent and dovecot as an IMAP/POP3 server. We would like you to perform the following steps:

Install and configure ```postfix``` on Stork DC mail server.

Create an email account ```mariyam@stratos.xfusioncorp.com``` identified by ```B4zNgHA7Ya```.

Set its mail directory to ```/home/mariyam/Maildir```.

Install and configure ```dovecot``` on the same server.

```
rpm -qa | grep postfix
yum install postfix -y
yum install dovecot -y
vi /etc/postfix/main.cf
  :set nu
  myhostname = stmail01.stratos.xfusioncorp.com
  mydomain = stratos.xfusioncorp.com
  myorigin = $mydomain
  inet_interfaces = all
  #inet_interfaces = localhost
  #mydestination = $myhostname, localhost.$mydomain, localhost
  mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain
  mynetworks = 172.16.238.0/24, 127.0.0.0/8
  home_mailbox = Maildir/

systemctl start postfix               #if gives error then comment out ::1 from /etc/hosts to disable ipv6
systemctl status postfix
useradd mariyam
passwd mariyam
telnet stmail01 25
    EHLO localhost
    mail from:mariyam@stratos.xfusioncorp.com
    rcpt to:mariyam@stratos.xfusioncorp.com
    DATA
    test mail
    .
    quit
mailq
su - mariyam
mailq
cat /home/mariyam/Maildir/new/1685105549.V1000058I685800bM925404.stmail01.stratos.xfusioncorp.com
exit
vi /etc/dovecot/dovecot.conf
  :set nu
  protocols = imap pop3 lmtp
vi vi /etc/dovecot/conf.d/10-mail.conf
  :set nu
  mail_location = maildir:~/Maildir
vi /etc/dovecot/conf.d/10-auth.conf
  :set nu
  disable_plaintext_auth = yes
  /auth_mechanisms
  auth_mechanisms = plain login
vi /etc/dovecot/conf.d/10-master.conf
  :set nu
  /unix_listener
  user = postfix
  group = postfix
systemctl start dovecot
systemctl status dovecot
telnet stmail01 110
    user mariyam
    pass B4zNgHA7Ya
    retr 1
    quit
ss -tulnp
```



