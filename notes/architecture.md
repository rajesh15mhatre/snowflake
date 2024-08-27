# Data Warehouse 
- A data warehouse is created by combiing and optimizing multiple operational (HR/Sales) data sources for analysis and reporting
- First we extract raw data from opearational DB to avoid impacting production in stage layer
- Then we integrate, clean, transform data and establish relationships in integation layer
- then we have access layer use by downstream like reporting, data science or other in access layer

# Cloud computing
- We don't have to worry about Physical/Virtual machine and storage all managed by cloud provider
- We don't have to manage sofware, data , OS all managed by SnowFlake
- We just have to manage application and tables

 # Snowflake features/editions
 - Standard : intro level. Complete DWH, data encryption, support of broad data types, time travel, DR for 7 days, network policy, secure data share, Fedrated auth & SSO, premier support 24/7
 - Enterprise: for large scale enterprise.Provides All standard features, multi-cluster WH, Time travel 90 days, materialize view, Search Optimization, Column level security, 24hrs early access to weekly release
 - Business critical: higher protection for extreamly sensitive data. Provides all Enterprise Features, additional security feature like Customer encryption, support for data specific regulation, DB failover DR
 - Virtual private: highest level security. Provides all Business critical features, dedicated virtual server with isolated env, dedicated metadata store, snowflake account

# snowflake price
- 

