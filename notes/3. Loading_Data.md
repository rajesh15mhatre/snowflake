# Loading Data
Two types of loading
- Bulk Loading - copy command
- Continuous LOading - snowpipe

# Understanding stages
- SF has stage a database object so do not confuse it with WH staging.
- It store source data location and access settings
- two types of Stages
  - External: like s3, GCP, Azure. if region is diff then additional charges applied
  - Internal : local SF storage

# Creating stage
```

// Create Database and schema
CREATE OR REPLACE DATABSE MANAGE_DB;
CREATE OR REPLACE SCHEMA external_stages;

// Create a external stage
CREATE OR REPLACE STAGE MANAGE_DB.external_stages.aws_stage
    url='s3://buketsnowflake3'
    credentials=(aws_key_id='ABCD'
    aws_secret_key='1123');

// desc of created stage
DESC STAGE MANAGE_DB.external_stages.aws_stage

// Alter stage
ALTER STAGE aws_stage
    SET credentials=(aws_key_id='XYZ'
    aws_secret_key='987');
// public stage doesn't have credentials
CREATE OR REPLACE STAGE MANAGE_DB.external_stages.aws_stage
    url='s3://bucketsnowflake3';

// List files in stage use @
LIST @aws_stage;

// Load data using copy command
COPY INTO OUR_FIRST_DB.PUBLIC.OPDERS
    FROM @aws_stage
    file_format=(type = csv field_delimiter=',' skip_header=1)
    pattern='.order.*';


   
```
