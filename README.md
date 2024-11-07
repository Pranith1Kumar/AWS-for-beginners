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

Step 5: Create IAM Group and Add User 
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

### Network config
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
