The Nautilus application development team recently finished the beta version of one of their Java-based applications, which they are planning to deploy on one of the app servers in Stratos DC. After an internal team meeting, they have decided to use the ```tomcat application server```. Based on the requirements mentioned below complete the task:

a. Install tomcat server on ```App Server 1``` using ```yum```.
b. Configure it to run on port ```6000```.
c. There is a ```ROOT.war``` file on Jump host at location ```/tmp```. Deploy it on this tomcat server and make sure the webpage works directly on base URL i.e without specifying any sub-directory anything like this http://URL/ROOT .

```
# on jump host
scp /tmp/ROOT.war tony@stapp01:/tmp
# on stapp01
yum install tomcat -y
cp /tmp/ROOT.war /usr/share/tomcat/webapps/
vi /usr/share/tomcat/server.xml
# change port from 8080 to 6000
systemctl start tomcat
```
