Relasjonsdatabaser: Skjema for å definere forhold og tabeller osv.
Verktøy som ser på skjemaene og jobber ut ifra det.

Ikke bruke relasjonsdatabase til alt av tekst, bibliotek.
Eller all Spotify lyd.

Musikken i seg selv eller teksten er ikke strukturert. 

- Big data isa concept
- Similar to small data, but much bigger
- Bigger problems, and solutions.
- Requires new tools and techniques. 
- Solves new problems.. and old problems differently

3V, 4V, 5V,
Volume
	Data at rest
		terabytes to exobytes of existing data to process
Velocity
	Data in motion
		Streaming data quick response
Variety
	Data in many forms
		Structured, unstructured, text , multimedia.
Veracity | trustworthyness
	Data in Doubt
		Data inconsistency, incompleteness, ambiguity, latency
		Interpolation. Hvis noe er generert, hva kan man stole på. 
Value
	Data into Money
		Business models can be mapped to the data.

![[Pasted image 20250306144428.png]]
Applications
Analytics engines.
Netflix used to know what would be a banger.

Denormalisere for å speede opp, siden kartesisk produkt er dyrt. JOINS
- NOSQL
	- MongoDB; CouchDB, Cassandra, Redis, BigTable, Hbase, Hypertable, Voldermort, Riak, Zookeeper.
- MapReuce
	- Hadoop, Hive, Pig, Cascading, Cascalog, mrJob, Caffeie, S2, MapR, Acunum, Flume, kafka, Azkaban, Oozie, Greenplum
- Storage
	- S3, HDFS, IBM, GPFS, EMC's Isilon OneFS, MapR FS.
- Platform (as a service)
	- Ec2, Google app engine, aws, bluemix
- Bluemix
	- Spark, R, Yahoo!, Mecanical Turl, Solr-Lucne, Elastic Search, Datameer, BigSheets, TinkerPop, AI

*Relational databases*
Pros
	Persitence/Consistence
	SQL
		Most people in the field know it.
	Integration
		Every programming language had a module for interacting with SQL. 
	Transactions
	Reporting
		A lot of tools for reporting. Autogenerate reports.
Cons
	Programming objects are in-memory structures.
		Stripped down to fit columns and rows
		Impedance mismatch problems
		Mismatch related to OO concepts
		Missing datatypes (e.g. pointers)
- Scale up vs scale out.
- More expensive vs more.
- Volume vs cost ratio too high
- Traditional RDBMS not designed for scale out. Its designed for scale up
- Traditional design for big boxes, not many boxes
- Slice and dice
	- Måten man putter inn data er uavhengig av måten man henter ut data.

- Conceptt that include
	- non relational
	- open source
	- cluster firendly
	- share nothing approach, dont share unecessari informatiuon about user
	- stateless, about other computers or clients.
	- schema-less
	- 21st century web enabled.
		often use JSon or URL strings, not SQL.

NoSQL/BigData Exceptations.
Must support partial failure.
	not one server destroy for every other server, could be thousands of servers.
- No loss of data due to failure
- System must deliver even if one component fails.
- Hot swapping components
- End result shall not be affected by partial failure.
- Must yield results during overloading.

Why so failure tolerant.
1000 servers and 5% failure means 50 servers a year.
Therefore often better two have a lot of low end servers instead of a few high end.

- Large scale data
	- Support multi cluster
- Support the development process
	- Better support for domain models
	- Aggregates, Aggregerer data.
	- Easier to use (might be complex to set up)
- Database is no longer an integration platform.
	- Retain data instead of processing it.

- NoSQL
	- Document stores
	- Column family
	- Key value store
	- Graph
![[Pasted image 20250306154116.png]]

# Document store
- structure: key value
	- Value can be a searchable field
- Can retrieve partial values
- Uses implicit schema, XML json bson
-  + event logs, contentmanagement
- - complex transactions, no acid support, queries may vary.
MongoDB, RavenDB, CouchDB
![[Pasted image 20250306154343.png]]
# Column family
- structure: key value
- key is a set of columns
- more complex but greater flexilibility
- + Eventlogging, real, time analytics, CMS, user experience
- - no ACID, SUM, AVG
- Cassandra.
![[Pasted image 20250306154537.png]]
• Column – simples storage unit  
• Super Column – smallest  
collection of combined columns  
• Column family – row that contain  
only one super column  
• Super Column family – a row that  
contain multiple super column.

# Key Value store
- structure: key value
- + session information, shopping cart, user porfile, sensor data aquisition
- - relation between data, multi key and transactions, set operations (no more than one key), value based queries.
- RIAK Redis MemCache (not persistent
![[Pasted image 20250306154731.png]]
# Graph Stores
- structure: simple (atomic) nodes that are connected
- + handle relations between nodes and moves between the nodes, uber on relations, may support ACID
- - aggregated DATA
- Neo4J, Caylay, Apache JENA.


# A lot of data timestamps
id, blob, binary large object.
2025.03.06,  >....................>


# Aggregate oriented stores
- supported by 
	- Document store
	- Column store
	- key value store
- works wewll when the root node is always the same
- if you want to slice and ddice the data, stick with relational databases -> change query.

![[Pasted image 20250306155215.png]]
How would you store this in key value.

OPC, or historian. Dependent on the frequency of the data insertions.
![[Pasted image 20250306155301.png]]

# ODATA
Open Data protocol
	Counterpart of RDF, sparQL
- HTTP/REST
- Human readable
- finnes biblioteker for de fleste språk
- HTTP/GET metoden for å spørre etter data.
- HTTP-POST for å legge til data.
- HTTP-DELETE for å slippe data

# REpresentational State Transfer
- Lightweight Architectural style for providing standards bteween computer systems on the web.


- 
