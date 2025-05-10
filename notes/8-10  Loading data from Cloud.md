This section covers how we can create different cloud accounts and load data into snowflake.

# 8 AWS DATA LOAD
```
// Create storage integration object

create or replace storage integration s3_int
  TYPE = EXTERNAL_STAGE
  STORAGE_PROVIDER = S3
  ENABLED = TRUE 
  STORAGE_AWS_ROLE_ARN = ''
  STORAGE_ALLOWED_LOCATIONS = ('s3://<your-bucket-name>/<your-path>/', 's3://<your-bucket-name>/<your-path>/')
   COMMENT = 'This an optional comment'
   
// See storage integration properties to fetch external_id so we can update it in S3
DESC integration s3_int;

// Create table first
CREATE OR REPLACE TABLE OUR_FIRST_DB.PUBLIC.movie_titles (
  show_id STRING,
  type STRING,
  title STRING,
  director STRING,
  cast STRING,
  country STRING,
  date_added STRING,
  release_year STRING,
  rating STRING,
  duration STRING,
  listed_in STRING,
  description STRING )
  
// Create file format object
CREATE OR REPLACE file format MANAGE_DB.file_formats.csv_fileformat
    type = csv
    field_delimiter = ','
    skip_header = 1
    null_if = ('NULL','null')
    empty_field_as_null = TRUE;
    
    
 // Create stage object with integration object & file format object
CREATE OR REPLACE stage MANAGE_DB.external_stages.csv_folder
    URL = 's3://<your-bucket-name>/<your-path>/'
    STORAGE_INTEGRATION = s3_int
    FILE_FORMAT = MANAGE_DB.file_formats.csv_fileformat

// Use Copy command       
COPY INTO OUR_FIRST_DB.PUBLIC.movie_titles
    FROM @MANAGE_DB.external_stages.csv_folder
        
// Create file format object
CREATE OR REPLACE file format MANAGE_DB.file_formats.csv_fileformat
    type = csv
    field_delimiter = ','
    skip_header = 1
    null_if = ('NULL','null')
    empty_field_as_null = TRUE    
    FIELD_OPTIONALLY_ENCLOSED_BY = '"'    
    
    
SELECT * FROM OUR_FIRST_DB.PUBLIC.movie_titles
    
```


# 9 AWS DATA LOAD
```

USE DATABASE DEMO_DB;
-- create integration object that contains the access information
CREATE STORAGE INTEGRATION azure_integration
  TYPE = EXTERNAL_STAGE
  STORAGE_PROVIDER = AZURE
  ENABLED = TRUE
  AZURE_TENANT_ID = '9ecede0b-0e07-4da4-8047-e0672d6e403e'
  STORAGE_ALLOWED_LOCATIONS = ('azure://storageaccountsnow.blob.core.windows.net/snowflakecsv', 'azure://storageaccountsnow.blob.core.windows.net/snowflakejson');

  
-- Describe integration object to provide access
DESC STORAGE integration azure_integration;

  
---- Create file format & stage objects ----

-- create file format
create or replace file format demo_db.public.fileformat_azure
    TYPE = CSV
    FIELD_DELIMITER = ','
    SKIP_HEADER = 1;

-- create stage object
create or replace stage demo_db.public.stage_azure
    STORAGE_INTEGRATION = azure_integration
    URL = 'azure://storageaccountsnow.blob.core.windows.net/snowflakecsv'
    FILE_FORMAT = fileformat_azure;
    

-- list files
LIST @demo_db.public.stage_azure;


---- Query files & Load data ----

--query files
SELECT 
$1,
$2,
$3,
$4,
$5,
$6,
$7,
$8,
$9,
$10,
$11,
$12,
$13,
$14,
$15,
$16,
$17,
$18,
$19,
$20
FROM @demo_db.public.stage_azure;


create or replace table happiness (
    country_name varchar,
    regional_indicator varchar,
    ladder_score number(4,3),
    standard_error number(4,3),
    upperwhisker number(4,3),
    lowerwhisker number(4,3),
    logged_gdp number(5,3),
    social_support number(4,3),
    healthy_life_expectancy number(5,3),
    freedom_to_make_life_choices number(4,3),
    generosity number(4,3),
    perceptions_of_corruption number(4,3),
    ladder_score_in_dystopia number(4,3),
    explained_by_log_gpd_per_capita number(4,3),
    explained_by_social_support number(4,3),
    explained_by_healthy_life_expectancy number(4,3),
    explained_by_freedom_to_make_life_choices number(4,3),
    explained_by_generosity number(4,3),
    explained_by_perceptions_of_corruption number(4,3),
    dystopia_residual number (4,3));
    
    
COPY INTO HAPPINESS
FROM @demo_db.public.stage_azure;

SELECT * FROM HAPPINESS;

```

## 10 GCP DATA LOAD
```
-- create integration object that contains the access information
CREATE STORAGE INTEGRATION gcp_integration
  TYPE = EXTERNAL_STAGE
  STORAGE_PROVIDER = GCS
  ENABLED = TRUE
  STORAGE_ALLOWED_LOCATIONS = ('gcs://bucket/path', 'gcs://bucket/path2');

  
-- Describe integration object to provide access
DESC STORAGE integration gcp_integration;

---- Query files & Load data ----

--query files
SELECT 
$1,$2,$3,$4,$5,$6,$7,$8,$9,$10,$11,
$12,$13,$14,$15,$16,$17,$18,$19,$20
FROM @demo_db.public.stage_gcp;


create or replace table happiness (
    country_name varchar,
    regional_indicator varchar,
    ladder_score number(4,3),
    standard_error number(4,3),
    upperwhisker number(4,3),
    lowerwhisker number(4,3),
    logged_gdp number(5,3),
    social_support number(4,3),
    healthy_life_expectancy number(5,3),
    freedom_to_make_life_choices number(4,3),
    generosity number(4,3),
    perceptions_of_corruption number(4,3),
    ladder_score_in_dystopia number(4,3),
    explained_by_log_gpd_per_capita number(4,3),
    explained_by_social_support number(4,3),
    explained_by_healthy_life_expectancy number(4,3),
    explained_by_freedom_to_make_life_choices number(4,3),
    explained_by_generosity number(4,3),
    explained_by_perceptions_of_corruption number(4,3),
    dystopia_residual number (4,3));
    
    
COPY INTO HAPPINESS
FROM @demo_db.public.stage_gcp;

SELECT * FROM HAPPINESS;
```
