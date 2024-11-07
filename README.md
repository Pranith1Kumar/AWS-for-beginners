# AWS_Exercises
This repo consists of beginner level tasks which can be help you to build your cloud fundamentals strong. 

## Exercises

## IAM AWS: Create a User
As you undoubtedly already know, working with the root account in AWS is not advised. As a result, you will establish a new account to serve as the administrator on a regular basis.

Create a user using the password credentials.

Add the newly formed user to a group called "admin" and attach the policy called "Administrator Access".

Ensure the user has a tag named Role with the value DevOps.

### solution: 
Solution
1.Go to the AWS IAM service.
2.Click on "Users" on the right side menu (just under "Access Management").
3.Click the button "Add users"
4.Insert the user name (e.g., Munna bhai).
5.Choose the credential type: "Password".
6.Set the console password to "custom" and click "Next".
7.Click "Add user to group"
8.Insert "admin" as the group name.
9.Check the "AdministratorAccess" policy and click "Create group".
10.Click "Next: Tags"
11.Add a tag with the key Role and value DevOps.
12.Click on "Review" and then "Create User"

