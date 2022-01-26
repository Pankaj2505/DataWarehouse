---
layout: post
title:  "Objective of DataWarehouse"
date:   2021-10-04 09:04:08 +0530
categories: Notes
permalink: '/datawarehouse/objective'
---

### Topic to Cover
- Architecture of Datawarehouse
- How to store operational data
- Centralize data warehouse
- Enterprise Data warehouse

#### Architecture of Datawarehouse
- Centralize data warehouse
    -Having a single database to support BI 
- Data Marts
     – small scale DW
- Component based warehouse
    -Multiple components like DW and data marts work together. And there are many DW and DM.
- Cubes
    - Special type of Database

### How to Store Operational Data
    - OLAP
        - This store the analytical data
        - we copy data from transactional system to OLAP server to run analytical and reporting operations
    - OLTP
        - It stores all the transactional data
        - for example storing pos data at the time of transaction happening
    - Layers  
        - Staging layer  
            - Persistent (Keep older data)  
            - Non – Persistent (Delete Older data)  


### Centralize data warehouse
    - Only one database is needed, which fetch data from multiple sources
    - One stop shopping, users uses single database for task like BI , report creation 

    - Challenges with Relational data warehouse
        - Technology
        – RDB face challenges with Data Volume
        - Design Engineering and data model
        - Internal Organization, Internal personal challenges 


    - solution Data Warehouse
        - Centralize
        - Default Option 
        - One Stop Shopping
        - Modern Technology
        - It requires High Degree of Inter Organizational Co-operation (no body wants to share data)
        - High data Governance
        - Ripple Effect – small change will affect other environment.

        -EDW Enterprise Data warehouse
            - Relational
            - Special Database (Cube)
        - Data Lake
            - Here we can use technology like Hadoop
            - Special Database (Cube)
        - Other (AWS S3, Google)
### Component-Based 
    -Decomposition
        - Divide Data into multiple components, we can isolate portion of data. This will helps to make some Datawarehouse private.

    - Mix and Match Decomposition
    - we can set up new DW with latest technology , we can use new BI technologies on Newly set up DW.
    - Bolt Together Component
    - Overcome Org challenges (data Privacy, create a DW and use its data for building another DW)
    - Often Inconsistent Data
    - Difficult to Cross integrate the components .its difficult to have data mart from multiple Datawarehouse, as data will be inconsistent
###	Architected
    - DW+DM
    - Dependent DM (CIF) corporation integration factory(how has access to which part of data warehouse /Data mart)
    -Front End DM- Data will be moving from DM to DW
    - DM Only
    - DW Bus
###	Non-Architected
    - Federated EDW- all DataMart are part of a Datawarehouse
    - Including Multidimensional database or Cube in DW
    - Just like RDBMS is a source for DW, Cube can also be a data source.

### What is a cube?
•	It is not a RDBMS
•	It follows the idea of dimensionality
•	Alternative of DW, here we have facts and for context we have dimensionality.
•	IT possible we can have DW built on top of RDBMS but data mart are built on top of cube.
•	Or we can have mix and match, one DM is on RDBMS and other are on cube
Advantage 
•	Fast query response time
•	Modest data volumes
•	More vendor variation than RDBMS
Disadvantage
Less flexible than RDBMS

Role of Staging Layer
1.	Staging layer is a mirror copy of source system.
2.	we copy all columns with same data type from there sources to their respective staging table
3.	primary focus is on extract and we use it  Before user access layer
a.	User access layer. 
i.	It’s a DW or DM. 
ii.	all data modelling technique like star schema , snowflake schema , fact , dimension , fact table , dimension table, all work on user access layer.
b.	Source-- Extract  Staging-- Transform  DW (User access layer)
c.	Why we don’t transform the data in staging table directly
i.	If we have same software in source we can do it  else we have to do one to one mapping between source and staging.
ii.	If source is sql server / oracle we should have many to one.
4.	Two type of staging layer
a.	Persistent
i.	We add new data on top of existing data in staging table
b.	Non-Persistent
i.	We delete the existing data from staging table before loading the new data.
ii.	Advantage
1.	Less storage space required
iii.	Disadvantage
1.	Need to go back to the source system if rebuild of user access layer required.
2.	Data QA required source system 
Introduction to ETL
Compare ETL /ELT
a.	Extract, transform, load
i.	Data move from source---extract staging--TransformDW(user access layer) load in DW
ii.	Challenges
1.	Significant business analysis before adding the data in DW. This will need computing power in DW server
2.	Significant data modelling before loading the data
b.	Extract load, transform 
i.	In data lake  or big data
1.	Source—Extract  load (Data lake)  Transform ( DM or cube)
ii.	Advantage
1.	We can use computing for of our analytics server
2.	Schema on read / Schema on write
a.	Schema on write – Schema is already set before doing the any operation.
i.	Set table
ii.	Set primary key/foreign key
iii.	Create schema
iv.	Do operation like insert, select
b.	Schema on read-Create the schema when reading the data.
i.	It helps to store unstructured data.
ii.	Here we just need to store the data in database.
iii.	Later on you can read what ever you want to extract from this unstructured data.
3.	We can defer creation of schema by loading the data in database/data lake/aws s3 bucket
2.	So if we are using RDBMS Cube to build DW then we can use ETL only , incase we use BIGDATA technologies then we can use ELT also.
Variation of ETL
a.	 Initial ETL
i.	Do it one time only, at first time set up
ii.	You bring only relevant data 
iii.	Bring probably needed data for BI and analytics
iv.	Bring Historical data
v.	Only big data technologies bring all data
b.	Incremental ETL
i.	Do it in regular bases, incrementally refreshes DW
ii.	Bring new data
iii.	Bring modified data
iv.	You never delete the data, keep it for historical purpose. We will highlight that this data is no longer relevant 
v.	ETL Pattern
1.	Append
2.	In place Update. 
a.	You are not appending; you are going to existing data and update it.
b.	In dimension modelling, we use in place update for type 1 Slowly changing Dimension.
3.	Complete replacement
a.	Overwrite a portion of data
4.	Rolling append 
a.	Maintain a certain period of data, if you roil in the new data, you will delete the older data beyond some time limit.
Explore the Role of Data Transmission 
c.	Data Transmission Goal
i.	Uniformity – keep data uniform when reading from new source and keeping in existing DW
ii.	Restructuring- keep engineered data
d.	Common Transformation model (Two or more source, data will be extracted to single staging table)
i.	Data Value Unification 
1.	Transform values of column to keep it same , if it exist in different format in source DB. Ex. Abbreviation in DB1, complete name in DB2
ii.	Data type and size unification 
1.	String (20) in DB1, String (40) in DB2
iii.	De- Duplication 
1.	Verify in existing DW , if data is already copied from DB1. So check it based on some KEY.
iv.	Dropping column (Vertical slicing)
1.	Copy only relevant column
v.	Value – based row filtering ( Horizontal slicing )
1.	Filter the ROW . lets say we want to register only those student who have got 80% in 12th
vi.	Correcting Known Error
1.	If we know some error is coming in source data , then we can go and correct it using transformation , lets say if phone no contain + sign then remove it.
