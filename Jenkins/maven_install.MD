### Install & configure Maven build tool on Jenkins
Maven is a tool used to create code and turn your code into an artifact. This plugin is frequently used to incorporate continuous integration.
#### Prerequisites
1. Jenkins server

a) Setup Maven on Jenkins Server.

b) Install Maven Plugin on jenkins GUI.  

c) Configure Maven and Java.
```bash
 # Creating maven directory under /opt
 mkdir /opt/maven
 cd /opt/maven
 # downloading maven version 3.6.0
 wget http://mirrors.estointernet.in/apache/maven/maven-3/3.6.1/binaries/apache-maven-3.6.1-bin.tar.gz
 tar -xvzf apache-maven-3.6.1-bin.tar.gz
```
d) Setup Enviroment Variables.
JAVA_HOME, M2, M2_HOME
```bash
 # Creating maven directory under /opt
vi ~/.bash_profile
M2_HOME=/opt/maven/apache-maven-3.6.1
M2=$M2_HOME/bin
PATH=<Existing_PATH>:$M2_HOME:$M2
```
e) logoff and login to check maven version
```bash
mvn --version
```
