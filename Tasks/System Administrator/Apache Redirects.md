The Nautilus devops team got some requirements related to some Apache config changes. They need to setup some redirects for some URLs. There might be some more changes need to be done. Below you can find more details regarding that:

httpd is already installed on app server 3. Configure Apache to listen on port 5000.

Configure Apache to add some redirects as mentioned below:

a.) Redirect http://stapp03.stratos.xfusioncorp.com:<Port>/ to http://www.stapp03.stratos.xfusioncorp.com:<Port>/ i.e non www to www. This must be a permanent redirect i.e 301

b.) Redirect http://www.stapp03.stratos.xfusioncorp.com:<Port>/blog/ to http://www.stapp03.stratos.xfusioncorp.com:<Port>/news/. This must be a temporary redirect i.e 302.

```
vi /etc/httpd/conf/httpd.conf
    Listen 5000

vi /etc/httpd/conf/httpd.d/main.conf
<VirtualHost *:5000>
ServerName stapp03.stratos.xfusioncorp.com
Redirect 301 / http://www.stapp03.stratos.xfusioncorp.com:5000/
</VirtualHost>

<VirtualHost *:5000>
ServerName www.stapp03.stratos.xfusioncorp.com:5000/blog/
Redirect 302 /blog/ http://www.stapp03.stratos.xfusioncorp.com:5000/news/
</VirtualHost>

systemctl restart httpd
