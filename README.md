<h1>Jenkins Installation Lab</h1>


<h2>Description</h2>
This is the first part of my guide on installing Jenkins, an open-source tool that streamlines and automates software development processes. Jenkins offers excellent integration with a variety of AWS services, including CodeCommit, CodeDeploy, and EC2. In this section, we will walk you through the steps to set up Jenkins on an Amazon EC2 instance. You'll learn how to initiate the installation, configure Jenkins for optimal performance, and implement automatic scaling by adding Jenkins agents to handle larger builds efficiently.
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 

<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2)
- <b>AWS EC2 Instance</b>

<h2>Program walk-through:</h2>

<p align="center">
To get started, the first step is to generate your <b>Key Pair<b>! This essential tool will help you secure your data and establish a reliable connection. Let’s dive in!: <br/>
<img src="https://i.imgur.com/3itjC2S.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  
<br />
<br />
</b>Creating a Key Pair:</b> Here’s a quick overview of how to create a key pair in AWS! Whether it's for server access or encrypting sensitive info, a solid key pair is crucial. Follow these steps to get started!  <br/>
<br/>
		1. Enter name in alignment with your project <br/>
		2. Select Key Pair Type: RSA <br/>
		3. Select the Private key file format: .pem <br/>
		4. Tags are optional <br/>


<img src="https://i.imgur.com/fzdegNV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Creating a Virtual Private Cloud (VPC):</b> A Virtual Private Cloud (VPC) offers a secure, customizable network in the public cloud, enhancing control and efficiency while supporting disaster recovery and integration with on-premise systems.<br/>
<img src="https://i.imgur.com/WeEUO1k.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Creating a VPC Steps: <br/> 1. Select VPC and more <br/>
		2. Enter name in alignment with your project (name_vpc) <br/>
		3. Choose IPv4 CIDR block, preferably a 16 range <br/>
		4. Number of Availability Zones (AZs): Select 1 <br/>
		5. Number of public subnets & Number of private subnets: Select 1 <br/>
		6. Add public & private IP ranges: 0.0.1.0/24 & 0.0.11.0/24 <br/>
		7. Click Create VPC
<br/>
<img src="https://i.imgur.com/HJq3yls.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/7TH73fK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Creating a Security Group: In order to manage inbound and outbound network traffic for your resources, primarily EC2 instances, as well as other AWS services like RDS and Lambda a security group is needed.   <br/>
<img src="https://i.imgur.com/0xpleuu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Creating a Security Group Steps: <br/>
		1. Enter name in alignment with your project (name_sg) <br/>
		2. Select the VPC that you initially created.
		
<br/>
<img src="https://i.imgur.com/dAQLB4P.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 3. Click on "Add Rule" within Inbound rules <br/>
<img src="https://i.imgur.com/aRflMbF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 4. Within Inbound rules, select and add the following three Types (HTTP, SSH, Custom TCP) and Source (Anywhere-IPv4) <br/>
<img src="https://i.imgur.com/PukLAuk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 5. Outbound rules DO NOT TOUCH <br/>
<img src="https://i.imgur.com/91VSzhE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 6. Click Create security group
<img src="https://i.imgur.com/xGuGVE6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
Creating an Amazon EC2 instance:Launching an Amazon EC2 instance provides scalable computing power within the AWS cloud. It enables organizations to create and manage virtual servers, offering enhanced flexibility and control over their computing infrastructure.  <br/>
<img src="https://i.imgur.com/HigTLMO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/sydYUIb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Create an Amazon EC2 instance Steps: <br />
		1. Enter name in alignment with your project (name_ec2) <br />
		2. Make sure the Amazon Machine Image (AMI) you choose is Amazon Linux 2023 AMI 
<br/>
<img src="https://i.imgur.com/CJCKV0J.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
3. Verify the Instance type is a t2.Micro and select the Key pair name you've created earlier from the dropdown:  <br/>
<img src="https://i.imgur.com/1Ss2ah4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
		4. Click Edit within Network settings<br />
			i. Select the VPC you previously created (name_vpc)<br />
			ii. Select the Public Subnet within the Subnet section<br />
			iii. Select Enable within the Auto assign public IP section<br />
			iv. Within Firewall (security groups), choose Select existing security group<br />
      v. Within Common security groups, select the Security group you previously created (name_sg)<br/>
<img src="https://i.imgur.com/7uDwt4B.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
5. Review the Summary to ensure all proper settings are in place then:  <br/>
<img src="https://i.imgur.com/cvE5JVg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Connecting Jenkins to Ec2 Instance: Click on the Connect button on the instance screen.  <br/>
<img src="https://i.imgur.com/L2FDpjN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/b9w3pTL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
	Troubleshooting - No public IP address assigned
		** If you forget to Select Enable within the Auto-assign public IP section, you'll have to delete your EC2 instance and recreate it again.
  <br/>
<img src="https://i.imgur.com/bJGbozJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/3Gi9Gi8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
	Connecting Jenkins to Ec2 Instance via Amazon Linux Installation<br /> 
			1. Click on the Connection Type: Connect using EC2 Instance Connect button on the instance screen.
  <br/>
  <br/>
<img src="https://i.imgur.com/Doy79Vh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
			2. This code makes sure your software packages on the instance are current by running the following command for a quick software update.
[Step 1 - Add the following code: sudo yum update –y]  <br/>
<img src="https://i.imgur.com/8YII13O.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
			3. Use the following command to add the Jenkins repository.
			[Step 2 - Add the following code: 
			sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo]  <br/>
<img src="https://i.imgur.com/s4gJRsY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
			4. This code allows us the ability to import a key file from Jenkins-CI to allow installation from the package.
[Step 3 - Add the following code: sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key || Then sudo yum upgrade]  <br/>
<img src="https://i.imgur.com/kZcr1hq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
			5. This code allows us to Install Java
[Step 4 - Add the following code: sudo yum install java-17-amazon-corretto -y]  <br/>
<img src="https://i.imgur.com/UFMuyuO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
			6. This code allows us to install Jenkins.
[Step 5 - Add the following code: sudo yum install jenkins -y]  <br/>
<img src="https://i.imgur.com/JY43iCT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
			7. This code enable the Jenkins service to start at boot
[Step 6 -  Add the following code: sudo systemctl enable jenkins]  <br/>
<img src="https://i.imgur.com/xtZt4cl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
			8. This code starts Jenkins as a service
[Step 7 - Add the following code: sudo systemctl start jenkins]  <br/>
<img src="https://i.imgur.com/VHtZ9y8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
9. This code allows me to check the status of the Jenkins service 
			[Step 8 - Add the following code: sudo systemctl status jenkins]
<img src="https://i.imgur.com/f5yghzi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Time to Configure Jenkins (Part 1)<br/>
1) Connect to http://<your_server_public_DNS>:8080 from your browser. You will be able to access Jenkins through its management interface.  <br/>
a) Go back to your Amazon EC2 instance main page
Copy Public IPv4 DNS into a browser in the following manner http://<your_server_public_DNS>:8080<br/>
<img src="https://i.imgur.com/pDaBoC0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br/>
b) Copy Public IPv4 DNS into a browser in the following manner http://<your_server_public_DNS>:8080
<br />
<br />
<img src="https://i.imgur.com/LEa5IZU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br /> 
<br />
<img src="https://i.imgur.com/xWJc1Kq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
2) To gain access to password return to Linux machine and use the following code: sudo cat/var/lib/jenkins/secrets/initialAdminPassword  <br/>
<img src="https://i.imgur.com/VEj1CUg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://i.imgur.com/Levnl8k.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
3) Copy the password form the Linux output and paste it within the Administrator password location then click Continue
<img src="https://i.imgur.com/uDQH5JW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/b9abSNc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
</p>
