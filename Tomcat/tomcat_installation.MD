# 4. Integrating Tomcat server in CI/CD
steps

   a) Setup a Linux EC2 Instance

   b) Install Java
   
   c) Configure Tomcat
   
   d) start Tomcat Server

   e) Access Web UI on port 8080

Pre-requisites
   * Ec2 Instance with Java 11

1. Download tomcat packages from https://tomcat.apache.org/download-80.cgi onto /opt on EC2 instance
Note: Make sure you change <version> with the tomcat version which you download.
```bash
# Create tomcat directory
cd /opt
wget http://mirrors.fibergrid.in/apache/tomcat/tomcat-8/v8.5.35/bin/apache-tomcat-8.5.35.tar.gz
tar -xvzf /opt/apache-tomcat-<version>.tar.gz
```
2. give executing permissions to startup.sh and shutdown.sh which are under bin.
```bash
chmod +x /opt/apache-tomcat-<version>/bin/startup.sh 
chmod +x /opt/apache-tomcat-<version>/bin/shutdown.sh
```
3. create link files for tomcat startup.sh and shutdown.sh
```bash
ln -s /opt/apache-tomcat-<version>/bin/startup.sh /usr/local/bin/tomcatup
ln -s /opt/apache-tomcat-<version>/bin/shutdown.sh /usr/local/bin/tomcatdown
tomcatup
```
4. access tomcat application from browser on port 8080

http://<Public_IP>:8080

a) now application is accessible on port 8090. but tomcat application doesnt allow to login from browser. changing a default parameter in context.xml does address this issue
```bash
#search for context.xml
find / -name context.xml
```
b) above command gives 3 context.xml files. comment () Value ClassName field on files which are under webapp directory. After that restart tomcat services to effect these changes. At the time of writing this lecture below 2 files are updated.
```bash
/opt/tomcat/webapps/host-manager/META-INF/context.xml
/opt/tomcat/webapps/manager/META-INF/context.xml

# Restart tomcat services
tomcatdown  
tomcatup
```
c) Update users information in the tomcat-users.xml file goto tomcat home directory and Add below users to conf/tomcat-users.xml file.
```bash
 <role rolename="manager-gui"/>
 <role rolename="manager-script"/>
 <role rolename="manager-jmx"/>
 <role rolename="manager-status"/>
 <user username="admin" password="admin" roles="manager-gui, manager-script, manager-jmx, manager-status"/>
 <user username="deployer" password="deployer" roles="manager-script"/>
 <user username="tomcat" password="s3cret" roles="manager-gui"/>
 ```
 d) Restart serivce and try to login to tomcat application from the browser. This time it should be Successful.
