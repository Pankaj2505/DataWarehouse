---
layout: post
title:  "Dimension Modelling"
date:   2021-10-02 09:04:08 +0530
categories: datawarehouse
permalink: /:categories/:title
---

### Topic to Cover 
- Technique to store data in Database
- What is dimensional modelling
- Why Dimensional modelling
- what is ER model
- Difference with ER model
- Types of Dimension Model

1. Technique to store data in Database
	- Normal form model (ER model)
	- Dimensional model 

2. What is dimensional modelling ?
	- here we create logical design of database in terms of fact and dimesnion.

3.  WHY use Dimensional Modelling
-	Performance
	-	Scalable
		-	We can add new dimensional table, fact table
		-	We can create new dimension also
-	Faster query
	-	Data is not normalized, means duplicate rows will be present
	-	Common Schema used Star schema, Snow flake schema
-	Simplicity
	-	Every Business process will have there own dimensional modelling tables like HR, SALE
	-	Easy to understand.

4. What is ER model . 
	- here we deisgn multiple table and uses PF,FK to join them 

5. Difference in ER and Dimensional model 
	- ER model 
		- purpose - Transactional system 
		- Design - complex
		- operation - select, update, delete, insert
		- performance - good
		- bitmap index - not used .bit map index used for low cardinality system , mean column where distinct values are very . for high cardinality sytem we can use B-Tree
		- best use- less redundant data, increase data integreity (same data everywhere)

	- dimensional model 
		- purpose - Reporting system 
		- Design - simple
		- operation - mostly select
		- performance - better
		- bitmap index - heavily used .bit map index used for low cardinality system , mean column where distinct values are very low
		- best use- faster retrival .simpliity

6. Types of Dimensional model
	-	Star Schema
		1.	Here data from all the level of one hierarchy will go into same table
		2.	Other table will have other hierarchy.
		3.	Only one level away from fact table.
		4.	Data is not normalized.
	-	Snowflake Schema 
		1.	We will have as much table as much we have level in hierarchy 
		2.	One or more level away from a fact table.
		3.	Data is normalized.

	-.	Hierarchal vs Flat Dimension
		-	College  Department  Faculty
		-	Student -----Flat dimension


7. Difference between star and snow flake 

	1. Snow-Flake Schema
		- Normalization : can have normalized dimensional table
		- Maintenance : Less redundancy so less maintence
		- Query - Complex queries due to normalized tables
		- Join - more join due to normalization 
		- Usage - if you are concerned about integrity and duplication 
	

	2. Star Schema
		- Normalization : pure denormalized 
		- Maintenance : more  redundancy so more 	 maintence
		- Query - simple queries due to denormalized tables
		- Join - less join 
		- Usage - speed and performance is important than data integrity.

	
