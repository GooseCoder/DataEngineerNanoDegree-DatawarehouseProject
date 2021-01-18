# Cloud DataWarehouse Project: Song Play Analysis

## About Sparkify

Sparkify is a music streaming startup, very recently it has been increasing their user base and also the amount of content(songs) provided, there is a huge amount of data generated about user actions and preferences however those are stored mainly in log files. There are really important insights there, in order to extract them we need to collect the data into a DataWarehouse. The initial data is stored in an **AWS S3** bucket, the goal is to store the analytics database into a **AWS Redshift** cluster, by running a list of **SQL** statements inside python scripts that executes the Extract, Transform and Load process.

## Project Files

.
├── create_tables.py (extracts the data into the staging tables)
├── dwh.cfg (general aws configuration)
├── etl.py (transforms and loads the data into redshift)
├── README.md (this file)
└── sql_queries.py (the sql queries for the process)

## The ETL Process

The Transformation process is described below.

### 1.0 The initial dataset

The data sets are a collection of application json files stored into **S3 buckets**. One of the buckets stores information of songs and artists. The other one has logs of actions made by users of the application, user listening preferences and other insights. 

### 2.0 Extract the data into the staging database

Once the data is retrieved is loaded into a couple of staging tables to ease the ETL process, this is done using the COPY function. 

* **staging_songs** - songs and artists data
* **staging_events** - logs of user actions

### 3.0 Transform and Load the data into Redshift 

Using SQL QUERIES we transform the data and separate them into the following star schema: 

* **songplays** (Fact Table)- Data of song plays made by users
* **time** - (Dimension Table) A time dimension, can use multiple date units extracted from the songplays data.
* **users** - (Dimension Table) User specific data
* **songs** - (Dimension Table) Song information
* **artists** - (Dimension Table) Artist information

### How to use

### Setup

* First generate a new IAM user in your AWS account and give the AdministratorAccess role and policies.
* Copy the generated access key and secret key.
* Generate an IAM Role.
* Spin up a RedShift Cluster and get the DWH_ENDPOIN and `DWH_ROLE_ARN` and add the values to the dwh config file.

### Run the scripts

* If the previous steps has been fullfilled then the dwh config file is complete.
* First execute the create-tables.py script
```
$ python create-tables.py
```
* Then execute the etl.py script
```
$ python etl.py
```

