# **AWS Projects**
- [Project 1](https://github.com/Pranith1Kumar/AWS-for-beginners/tree/main/Data%20Analytics%20on%20AWS/Admission%20Enquiries%20Analysis).








# AWS_Exercises
This repo consists of beginner level tasks which can be help you to build your cloud fundamentals strong. 

### Exercises

## 1. IAM AWS: Create a User
As you undoubtedly already know, working with the root account in AWS is not advised. As a result, you will establish a new account to serve as the administrator on a regular basis.
Create a user using the password credentials.
Add the newly formed user to a group called "admin" and attach the policy called "Administrator Access".
Ensure the user has a tag named Role with the value DevOps.

## Steps to Create an IAM User
Step 1: Access the IAM Service
1. Log in to your AWS Management Console.
2. In the search bar, type **IAM** and select **IAM** from the services list.

Step 2: Navigate to Users
1. In the left sidebar, click on **Users** under the **Access Management** section.

Step 3: Add a New User
1. Click the **Add users** button.

Step 4: Enter User Details
1. In the **User  name** field, enter the desired username (e.g., `Munna bhai`).

Step 5: Choose Credential Type
1. Under **Select AWS access type**, check the box for **Password**.
2. Set the console password to **Custom password** and enter your desired password.
3. Click **Next: Permissions**.

Step 6: Add User to Group
1. Click on **Add user to group**.
2. In the **Group name** field, enter `admin`.
3. Check the box for the **AdministratorAccess** policy.
4. Click **Create group**.

Step 7: Add Tags (Optional)
1. Click **Next: Tags**.
2. Click **Add tag**.
3. In the **Key** field, enter `Role`.
4. In the **Value** field, enter `DevOps`.

Step 8: Review and Create User
1. Click **Next: Review**.
2. Review the user details and permissions.
3. Click **Create user**.

Step 9: Save User Credentials
1. After the user is created, you will see a success message.
2. Make sure to save the user’s access key and secret access key if applicable, as you will not be able to see them again.


## 2. Creating an IAM User with Permissions
AWS Identity and Access Management (IAM), your task is to create a new IAM user who will have the necessary permissions to manage resources in Amazon EC2, DynamoDB, Lambda, and S3. You will achieve this by using both a directly attached policy and an inline policy. Additionally, the new user should be added to an IAM group named Core Services to simplify permission management.

Step 1: Log in to AWS Management Console
1. Go to the [AWS Management Console](https://aws.amazon.com/console/).
2. Enter your AWS account credentials to log in.

Step 2: Navigate to IAM Service
1. In the search bar at the top, type `IAM` and select **IAM** from the dropdown list.

Step 3: Create a New IAM User
1. In the left sidebar, click on **Users**.
2. Click the **Add users** button.
3. In the **User  name** field, enter a unique username (e.g., `newUser `).
4. Under **Access type**, check the box for **AWS Management Console access**.
5. Set a Console password (you can choose to require the user to reset the password upon first login).
6. Click **Next: Permissions**.

Step 4: Set Permissions
A. Directly Attach Policy
1. On the **Set permissions** page, select **Attach existing policies directly**.
2. In the search box, type `AmazonS3FullAccess`.
3. Check the box next to **AmazonS3FullAccess** to grant full access to S3.

B. Create Inline Policy
1. Click on **Next: Tags** (you can skip adding tags for now).
2. Click **Next: Review**.
3. Click **Create user**.

Step 5: Add Inline Policy for EC2 Management
1. After the user is created, click on the user’s name to go to the user details page.
2. Click on the **Permissions** tab.
3. Click on **Add inline policy**.
4. Select the **JSON** tab and enter the following policy to allow starting and stopping EC2 instances:
````
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "Statement1",
			"Effect": "Allow",
			"Action": [
				"ec2:*"
			],
			"Resource": [
				"*"
			]
		}
	]
}
````

Click on Review policy.
Give the policy a name (e.g., EC2StartStopPolicy) and click Create policy.

Step 5: Create IAM Group and add an User 
1. In the left sidebar, click on Groups.
2. Click the Create New Group button.
3. In the Group name field, enter Core Services.
4. Click Next Step (you can skip attaching policies for now).
5. Click Create Group.
6. Go back to the Users section and select the user you created (e.g., newUser ).
7. Click on the Groups tab.
8. Click Add user to groups.
9. Check the box next to Core Services and click Add to groups.

Step 6: Review and Save 

## 3. Launch an general purpose EC2 instance using IAM User.
Your task is to create and configure an EC2 instance using the AWS Management Console. Begin by selecting an appropriate Ubuntu AMI and generating a key pair for secure SSH access. Carefully configure the instance to meet specified requirements, ensuring compliance with cloud security and resource management best practices. Focus on aspects such as instance type, security group settings, and network configuration to align with security standards and optimal resource utilization. This exercise emphasizes the importance of precision in deployment and effective use of AWS tools to manage cloud resources securely and efficiently.

1. Log in to the AWS Management Console:
2. Navigate to the AWS Management Console.
3. To log in, provide your IAM user credentials.
4. Navigate to the EC2 dashboard:
In the AWS Management Console, locate and choose "EC2" from the "Services" menu.

### Launch Instance:
1. In the EC2 Dashboard, click the "Launch Instance" button.
2. Select an Amazon Machine Image (AMI):
3. In the "Choose an Amazon Machine Image (AMI)" option, look for "Ubuntu."
4. Choose the required Ubuntu AMI (for example, Ubuntu Server 20.04 LTS).
5. Choose an instance type.
6. In the "Choose an Instance Type" section, pick a general-purpose instance type (t2.micro,t2 family) that falls within the free tier.
7. Go to "Next: Configure Instance Details."

### Key pair for login
Key pair is used to login/connect to instance via ssh through cli, which is a encrypted file contains sha code.

1. Create a keypair give a name to key pair
2. Use keypair type rsa which is publicly available, if not you can create a ED25519 for private use.
3. Create Private key file format
.pem
For use with OpenSSH you can use 
.ppk
For use with PuTTY
4. Here I need a .pem for my instance so I genareate a rsa with .pem format.
5. After keypair is generated the .pem is downloaded which contains the encryption code.

### Network configuration
1. Ensure that the security group has allowed the ingress traffic only with ssh.
### Configure Instance Details:
1. Maintain the default settings for the number of instances and network.
2. If you wish to access the instance over the internet, make sure the "Auto-assign Public IP" option is activated.
3. Click "Next: Add Storage."

### Add storage:
1. In the "Add Storage" section, you will find a default root volume.
2.Set the size to 8 GB and make sure the volume type is General Purpose SSD (gp2).
3. Select "Next: Add Tags."

### Review and launch the instance.


### Accessing Your EC2 Instance.

There are 4 ways to connect to your instance.
### 1. EC2 instance connect.
This can be connect to your instance in aws console.

1. Open the AWS Management Console.
2. Access the AWS Management Console and log in.
3. Navigate to the EC2 dashboard:
4. Click "EC2" in the "Services" menu.
5. Select your instance.
6. Find and choose your currently running instance from the "Instances" section.
7. Click "Connect":
8. Click the "Connect" button at the top of the page.
9. Select "EC2 Instance Connect":
10. Choose the "EC2 Instance Connect" tab.
11. Connect:
12. Click on the "Connect" button. A new browser window will appear, giving you terminal access to your instance.

### 2. AWS Systems Manager Session Manager requires the following prerequisites:

1. The AWS Systems Manager agent must be installed on your instance (it is the default for Amazon Linux and Windows).
2. The instance must be located in a VPC with access to the Systems Manager endpoints.
3. The IAM role associated with the instance must have the required rights (for example, AmazonSSMManagedInstanceCore).
4. Open the AWS Management Console.
5. Access the AWS Management Console and log in.
6. Navigate to the EC2 dashboard:
7. Click "EC2" in the "Services" menu.
8. Select your instance.
9. Find and choose your currently running instance from the "Instances" section.
10. Click "Connect":
11. Click the "Connect" button at the top of the page.
12. Select "Session Manager":
13. Choose the "Session Manager" tab.
14. Start Session:
15. Click on the "Connect" button. A new browser window will open, allowing you to connect to your instance via terminal without the need for SSH.


### 3. SSH Client

1. Open the Terminal (Linux/Mac) or Command Prompt (Windows):
2. Go to the location where your key pair (.pem) file is placed.
3. Changing Permissions (Linux/Mac):
Run this command:
````
chmod 400 MyKeyPair.pem
````

4. Connect to your instance.
5. To connect, use the following command (replace your-public-ip with your instance's public IP address).
````
ssh -i "MyKeyPair.pem" ubuntu@your-public-ip
````
Congratulations! You have successfully launched and accessed an EC2 instance with an Ubuntu AMI and a gp2 volume.

### 4. EC2 Serial Console
The EC2 Serial Console is a text-based interface that lets you access the serial port of your Amazon EC2 instance. This capability is especially useful for debugging booting, network settings, and other system-level issues when standard SSH access is unavailable.


1. Accessing the EC2 Serial Console:
2. Open the AWS Management Console.
3. Access the AWS Management Console and log in.
4. Navigate to the EC2 dashboard:
5. Click "EC2" in the "Services" menu.
6. Select your instance.
7. In the "Instances" column, locate and pick the instance you wish to debug.
8. Click "Connect":
9. Click the "Connect" button at the top of the page.
10. Select "Serial Console":
11. Select the "Serial Console" tab.
12. Connect:
13. To open a session with the serial terminal, click the "Connect" button.






# DATABASES IN AWS

A database is responsible for storing structured and semi-structured data. There are two mainly two types of databases:

1. Relational: A relational database stores structured data in tabular format (rows and columns). Its functionalities include:
    
    ![image](https://github.com/user-attachments/assets/9d986bd0-6b5b-41ac-b15d-1246e5c8771c)

    
    1. Specialised query language for retrieval (SQL) 
    
    ```sql
    SELECT first_name, last_name FROM customers WHERE city = 'Chicago' ORDER BY last_name;
    ```
    
    1. Using B-trees for indexing in databases.
    
    ![image (1)](https://github.com/user-attachments/assets/dda24b54-4771-4ea0-830f-bea7dee5c89f)

    
    1. Usage of joins to retrieve data from multiple tables.
2. Non-Relational: A non-relational database stores semi-structured data and is more flexible than relational. It allows every item to have any number of fields. Non-relational databases are classified into different types:
    1. Key-value Pair
    2. document database
    3. Graph database
    4. Columnar oriented / Column-Family
    
    
    ![image (2)](https://github.com/user-attachments/assets/bfa46970-dd95-465e-828f-066df8115eca)


## AWS DATABASE SERVICES

AWS provides a range of services to support both SQL and NO-SQL databases.

![image (3)](https://github.com/user-attachments/assets/6f8ad398-93b7-4a2b-809d-f29c83b86792)


Based on the use-case different services can be used, however, the most popular databases on AWS are RDS and DynamoDB.

### AMAZON RDS

Amazon RDS is used for creation of relational databases. It supports multiple SQL engines:

1. MySQL
2. Oracle
3. PostgreSQL
4. IBM DB2
5. Mircosoft SQL Server
6. MariaDB
7. Aurora (MyAlSQL compatible) - Amazon’s own version of mysql and is said to have 5 times more throughput than MySQL
8. Aurora (Postgres compatible) - Amazon’s own version of postgreSQL and is said to have 3 times more throughput than PostgreSQL.

### Steps to create a database on RDS

1. Go to the AWS management console, on the search bar, search **RDS**.
2. The **dashboard** of RDS opens up. On the top right corner, choose the **ap-south-1 (Mumbai) region.**
3. On the dashboard, choose **DB instances.**
4. All the databases in the region get displayed, click **Create Database.**
5. For **Choose a database creation method**, choose **Standard Create.**
6. For **Engine Options**, any sql engine can be chosen, but we are going for **MySQL**.
7. Keep all the **engine version settings** to be default.

![image (4)](https://github.com/user-attachments/assets/e4dd106f-15f7-444a-8cac-b45a3f0840c9)


8. Under **Templates**, based on the use-case required template is chosen. But we are going for **Free Tier.** 
9. The **Availability and Durability** section is disabled for **Free Tier** and is defaulted to be **Single DB Instance.** 
10. Under **Settings**, name the db instance to your desired name, under **DB instance identifier**. Ensure you are following the constraints given for your db instance name.
11. Under **Credential Settings**, Give a **master username,** this name is used to login in to the database. Mostly “**admin**” is used. But any username can be given.
12. Under **Credentials management**, choose **Self managed**
13. Keep the **Auto generate password** checkbox **unchecked**.
14. Give the master password to login in to your database under **Master Password**
15. Under **confirm master password,** confirm the password
16. Leave the **Instance configuration** to have default settings, under **Burstable classes**, choose **db.t3.micro.**
![image (5)](https://github.com/user-attachments/assets/a706fe24-26e1-4ec8-8082-9c9caa15c1ba)



17. Under **Storage**, Select **General Purpose SSD (gp2)** under **Storage type**
18. Enter **20** for **Allocated Storage** (lowest amount of storage possible)
19. Under **Storage autoscaling**, **disable** the checkbox “**Enable storage autoscaling”**
20. Under **Connectivity,** under **compute resource**, Ensure “**Don’t connect to an EC2 compute resource**” is selected.
21. Keep the **VPC** to be **Default** in **Virtual Private Cloud (VPC)** and **subnet group** to be **default** in **DB subnet group**
22. Under **public access**, either “Yes” or “No” can be chosen, since this is just for practice, “**Yes**” can be chosen.
23. Under **VPC security group (firewall)**, Choose **existing** and let the **existing VPC security groups** be **default**
24. Under **Availability Zone**, keep the default option “**No Preference**”
25. Let the **RDS proxy** have **default settings**
26. For the rest of the configuration, keep them all default
27. At the bottom of the window, click **Create database**
28. The database gets created

### Connecting to the database

AWS doesn’t provide an interface to add rows and columns and tables to the database, to connect to this database, we can use MySQL Workbench locally and connect it to the endpoint.

To connect to the database on AWS we need:

1. Endpoint provided by database
    1. Go to RDS, on the left side panel, choose Databases
    2. Choose the database just created
    3. Under connectivity and Security, copy the endpoint given
2. Port number 
    1. port number is also available under connectivity and Security

![image (6)](https://github.com/user-attachments/assets/54b37edf-3a25-4a5a-9821-5da97342ce5e)


3. The username entered during creation of database
4. The password entered during creation of database

Steps

1. Go to Mysql Workbench/ Install it if not there on computer


<img width="960" alt="image (7)" src="https://github.com/user-attachments/assets/1b55aa40-f24f-479b-8630-f49467832f23">

2. Go to the Setup new connection wizard, enter a **connection name** (any name)
    1. under **connection method** choose **Standard (TCP/IP)** 
    2. under **hostname**, enter the endpoint saved before 
        1. ex- http://mysql-dbms.cd2g0wmugcda.ap-south-1.rds.amazonaws.com/ (this is just an example, please check your endpoint on the aws console)
    3. under **port**, enter the **port number saved before**
    4. enter **username** and **password** set up before
    5. **test connection**
    6. ensure that the **public access** is “**yes**” for db instance on the **aws console (if doesn’t work)**


![image (8)](https://github.com/user-attachments/assets/e48508df-33f6-4979-a014-6c4cc60d9aa6)

Connection has been established.

### Delete the db instance

1. Go to **Amazon RDS**, on the left side bar, choose **databases**
2. ensure you are in **ap-south-1 region**, check on top left corner (this is where the db instance has been created)
3. select the database you created
4. Go to **Actions**, choose **delete**
5. **Uncheck** the **Create Final snapshot**
6. **Uncheck** **Retain automated backups**
7. **Check** the “**I acknowledge that upon instance deletion, automated backups, including system snapshots and point-in-time recovery, will no longer be available**.”
8. Type delete me or whatever context that needs to be typed
9. click delete
