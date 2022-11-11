
# Setting up EC2 instance

1. Prerequisites

    EC2 Instance
    
     * With Internet Access
        
     * Security Group with Port 8080 open for internet

2. Create a key pair using Amazon EC2. If you already have one, you can skip to step 3.

3. Create a security group for your Amazon EC2 instance. If you already have one, you can skip to step 4.

4. Launch an Amazon EC2 instance.

5. Install and configure Jenkins.

6. Clean up tutorial resources.

### Creating a key pair

1. Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/ and sign in.

2. In the navigation pane, under NETWORK & SECURITY, select Key Pairs.

3. Select Create key pair.

4. For Name, enter a descriptive name for the key pair. Amazon EC2 associates the public key with the name that you specify as the key name. A key name can include up to 255 ASCII characters. It cannot include leading or trailing spaces.

5. For File format, select the format in which to save the private key.
    For OpenSSH compatibility, select pem.
    For PuTTY compatibility, select ppk.

6. Select Create key pair.

7. The private key file downloads automatically. The base file name is the name you specified as the name of your key pair, and the file name extension is determined by the file format you chose. Save the private key file in a safe place.

8. If you use an SSH client on a macOS or Linux computer to connect to your Linux instance, run the following command to set the permissions of your private key file so that only you can read it.

### Creating a security group
for this project, you will create a security group and add the following rules:

1. Allow inbound HTTP access from anywhere.

2. Allow inbound SSH traffic from your computer’s public IP address so you can connect to your instance.

To create and configure your security group:

3. Decide who may access your instance. For example, a single computer or all trusted computers on a network. For this tutorial, you can use the public IP address of your computer.

    a) To find your IP address, use the check IP service tool from AWS3 or search for the phrase "what is my IP address" in any search engine.

    b) If you connect through an ISP or from behind your firewall without a static IP address, you will need the range of IP addresses used by client computers. If you don’t know this address range, you can use 0.0.0.0/0 for this tutorial.

4. Sign in to the AWS Management Console.

5. Open the Amazon EC2 console by selecting EC2 under Compute.

6. In the left-hand navigation bar, select Security Groups, and then select Create Security Group.
 
7. In Security group name, enter WebServerSG or any preferred name of your choice, and provide a description.

8. Select your VPC from the list. You can use the default VPC.

9. On the Inbound tab, add the rules as follows:
    a) Select Add Rule, and then select SSH from the Type list.

    b) Under Source, select Custom, and in the text box, enter the IP address from step 1, followed by /32 indicating a single IP Address. For example, 104.34.241.123/32 is a single IP address, while 198.51.100.2/24 results in a range of 256 IP addresses.

    c) Select Add Rule, and then select HTTP from the Type list.

    d) Select Add Rule, and then select Custom TCP Rule from the Type list.

    e) Under Port Range, enter 8080.

10. Select Create.

### Launching an Amazon EC2 instance

To launch an EC2 instance:

1. Sign in to the the AWS Management Console.

2. Open the Amazon EC2 console by selecting EC2 under Compute.

3. From the Amazon EC2 dashboard, select Launch Instance.

4. The Choose an Amazon Machine Image (AMI) page displays a list of basic configurations called Amazon Machine Images (AMIs) that serve as templates for your instance. Select the HVM edition of the Amazon Linux AMI.
 
5. Scroll down and select the key pair you created in the creating a key pair section above or any existing key pair you intend to use.

    a) Select Select an existing security group.

    b) Select the WebServerSG security group that you created.

    c) Select Launch Instance.

6. In the left-hand navigation bar, choose Instances to view the status of your instance. Initially, the status of your instance is pending. After the status changes to running, your instance is ready for use.

