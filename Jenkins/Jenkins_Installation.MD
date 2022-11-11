# 2. Installing and configuring Jenkins
In this step you will deploy Jenkins on your EC2 instance by completing the following tasks:

### Connecting to your Linux instance
1. Select the instance and locate Public DNS.

2. Prerequisites
The tool that you use to connect to your Linux instance depends on your operating system.

   a) If your computer runs Windows, you will connect using PuTTY.

   b) If your computer runs Linux or Mac OS X, you will connect using the SSH client.
 
3. Using SSH to connect to your instance
   a) Open an SSH client.

   b) Locate your private key file. The key used to launch this instance is demo-project-keypair.pem

   c) Run this command, if necessary, to ensure your key is not publicly viewable.
      ```bash
      $ chmod 400 demo-project-keypair.pem
      ```

   d) Connect to your instance using its Public IP:
      18.196.179.155
      Example:
      ```bash
       ssh -i "demo-project-keypair.pem" ec2-user@18.196.179.155
      ```

4. Downloading and installing Jenkins
   a) Ensure that your software packages are up to date on your instance by uing the following command to perform a quick software update:

      ```bash
      $ sudo yum update –y
      ```

   b) Add the Jenkins repo using the following command:
      ```bash
      $ sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
      ```

   c) Import a key file from Jenkins-CI to enable installation from the package:
      ```bash
      $ sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
      $ sudo yum upgrade
      ```

   d) Install Java:
      ```bash
      $ sudo amazon-linux-extras install java-openjdk11 -y
      ```

   e) Install Jenkins:
      ```bash
      $ sudo yum install jenkins -y
      ```

   f) Enable the Jenkins service to start at boot:
      ```bash
      $ sudo systemctl enable jenkins
      ```

   g) Start Jenkins as a service:
      ```bash
      $ sudo systemctl start jenkins
      ```

   h) You can check the status of the Jenkins service using the command:
      ```bash
      $ sudo systemctl status jenkins
      ```
### Configure Git pulgin on Jenkins
Git is one of the most popular tools for version control system. you can pull code from git repositories using jenkins if you use github plugin.

#### Prerequisites
1. Jenkins server
   Install Git and Git packages on jenkins server
   ```bash
   $ yum install git -y
   ```
### Integrate maven with Jenkins
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
