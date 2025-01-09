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
