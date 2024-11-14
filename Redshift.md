A Petabyte scale Data Warehouse
OLAP not OLTP - This means it is column based

other systems put their data into redshift so that we can see trends over time (on columns)

Redshift Spectrum allows for direct query of S3 data (without getting it in to Redshift)

Based in **One AZ**
	Has a leader node - used for query input and aggregation
	Has multiple compute nodes - perform queries on data

Can use VPC Networking with Enhanced VPC Routing
![[Pasted image 20241010160627.png]]

Disaster Recovery
![[Pasted image 20241010160724.png]]