## *Project Steps for Admission Enquiries Analysis*

# Step 1: Data Preparation

1. Identify Tools for Data Visualization.
- Choose Visualization Tool: Use Amazon QuickSight (free-tier eligible).
- Define Key Attributes: Identify key metrics to visualize, such as admission trends, B.Tech score distributions, and interest areas. (My dataset link is attached below)
- [Dataset Link](https://www.kaggle.com/datasets/praneethkumar007/b-tech-students-interest-on-technologies)

If you want to create your dataset on your own below you can refer and start building your schema for the analysis.

Define the Dataset Schema
- Create Dataset: Structure a dataset for at least 8000 B.Tech students with the following attributes:
- Student_ID: Unique identifier
- Name: Full Name
- Department: B.Tech Specialization (CSE, ECE, ME, CE, etc.)
- CGPA: Absolute integer between 6 and 10
- Contact_Number: Random 10-digit number
- College_Email: Generated in the format: name@college.edu
- BTech_Score: Between 50 and 300
- Interest_Area: Courses like AI, ML, Cybersecurity, etc.

Action: Create a CSV file named admission_enquiries.csv with the above attributes filled with synthetic data.

# Step 2: AWS S3 Bucket Setup

1. Create an S3 Bucket
- Log in to AWS Management Console.
- Navigate to S3 and create a new bucket (e.g., `admission-enquiries-data`).

2. Upload the Dataset
- Upload the admission_enquiries.csv file to the created S3 bucket.

# Step 3: AWS Glue Setup

1. Create an AWS Glue Crawler
- Navigate to AWS Glue and create a new crawler.
- Set the data store to S3 and specify the bucket path.
  
2. Configure the Glue Crawler
- Choose to store the metadata in the AWS Glue Data Catalog.


# Step 3: AWS Glue Setup

1. Create an AWS Glue Crawler
- Navigate to AWS Glue and create a new crawler.
- Set the data store to S3 and specify the bucket path.

2. Configure the Glue Crawler
- Choose to store the metadata in the AWS Glue Data Catalog.

3. Run the Crawler
- Execute the crawler to generate schema information for the dataset.

# Step 4: AWS Redshift Cluster Setup

1. Create an Amazon Redshift Cluster
- Go to Amazon Redshift and create a new cluster (DC2.large, free-tier eligible).

2. Create a Database and Tables
- Use the Redshift console to create a database.
- Define the table structure to store student inquiries.

3. Load Data from S3 to Redshift
- Use the following SQL command to load data from S3:

```sql
COPY admission_enquiries
FROM 's3://admission-enquiries-data/admission_enquiries.csv'
IAM_ROLE 'arn:aws:iam::<your-account-id>:role/RedshiftRole'
FORMAT AS CSV IGNOREHEADER 1;
```

```
# look like
# COPY admission_enquiries
# FROM 's3://admission-enquiries-data/admission_enquiries_btech (1).csv'
# IAM_ROLE 'arn:aws:iam::8928*917****:role/RedshiftGlueS3Role'
# FORMAT AS CSV
# IGNOREHEADER 1;
```

# Step 5: Perform Analysis in Redshift
- SQL Queries for Insights
- Students who enquired for B.Tech admission

```
SELECT * FROM admission_enquiries WHERE department IS NOT NULL;
```

Students interested in B.Tech Computer Science

```
SELECT * FROM admission_enquiries WHERE department = 'CSE';
```

Students with BTech_Score above 100

```
SELECT * FROM admission_enquiries WHERE BTech_score > 100;
```

Students interested in Civil Engineering

```
SELECT * FROM admission_enquiries WHERE department = 'CE';
```

Students with interest in AI & BTech_Score > 100:
sql

```
SELECT * FROM admission_enquiries WHERE interest_area = 'AI' AND BTech_score > 100;
```

# Step 6: Create Visualizations in Amazon QuickSight
1. Connect QuickSight to Redshift
- Go to QuickSight and connect it to your Redshift cluster.
2. Create Dashboards
- Develop dashboards for:
- Admission trends by department.
- BTech_score distribution.
- Top interest areas.






If you want to push to yout GitHub account follow below commands.

```
git init
git add .
git commit -m "Initial commit of Admission Enquiries Analysis project"
git remote add origin <repository-url>
git push -u origin main
```
