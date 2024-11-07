# AWS_Exercises
This repo consists of beginner level tasks which can be help you to build your cloud fundamentals strong. 

## Exercises

## IAM AWS: Create a User
As you undoubtedly already know, working with the root account in AWS is not advised. As a result, you will establish a new account to serve as the administrator on a regular basis.

Create a user using the password credentials.

Add the newly formed user to a group called "admin" and attach the policy called "Administrator Access".

Ensure the user has a tag named Role with the value DevOps.

### Solution:
## Steps to Create an IAM User

### Step 1: Access the IAM Service
1. Log in to your AWS Management Console.
2. In the search bar, type **IAM** and select **IAM** from the services list.

### Step 2: Navigate to Users
1. In the left sidebar, click on **Users** under the **Access Management** section.

### Step 3: Add a New User
1. Click the **Add users** button.

### Step 4: Enter User Details
1. In the **User  name** field, enter the desired username (e.g., `Munna bhai`).

### Step 5: Choose Credential Type
1. Under **Select AWS access type**, check the box for **Password**.
2. Set the console password to **Custom password** and enter your desired password.
3. Click **Next: Permissions**.

### Step 6: Add User to Group
1. Click on **Add user to group**.
2. In the **Group name** field, enter `admin`.
3. Check the box for the **AdministratorAccess** policy.
4. Click **Create group**.

### Step 7: Add Tags (Optional)
1. Click **Next: Tags**.
2. Click **Add tag**.
3. In the **Key** field, enter `Role`.
4. In the **Value** field, enter `DevOps`.

### Step 8: Review and Create User
1. Click **Next: Review**.
2. Review the user details and permissions.
3. Click **Create user**.

### Step 9: Save User Credentials
1. After the user is created, you will see a success message.
2. Make sure to save the user’s access key and secret access key if applicable, as you will not be able to see them again.


