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