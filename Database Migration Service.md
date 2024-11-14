---
aliases:
  - DMS
---
managed service which allows for 0 data loss, low or 0 downtime migrations between 2 database endpoints.

The service is capable of moving databases INTO or OUT of AWS.

Full load = copy everything in a db at a certain time stamp
Full Load + CDC = for replication which captures changes
CDC Only = use native tooling

No Schema Conversion inside DMS but AWS has Schema Conversion Tool (SCT)
	SCT is used when converting one db type to another

DMS can utilize snowball. This is a physical device that you can ship to AWS to upload onto an S3. DMS can then migrate the data from that S3

Different Modes
General Purpose and Max I/O Mode
	General purpose = default for 99.9% of uses
Standard and Infrequent access
Burst and Provisioned