A serverless interactive querying service that operates on [[S3]]

**Original data is never changed, it remains on S3**
![[Pasted image 20241010153548.png]]

There is no Athena infrastructure. It is all handled by AWS

Example Athena commands
```sql
# Create the Athena DB
CREATE DATABASE A4L;


# Create the Athena DB Table

CREATE EXTERNAL TABLE planet (
  id BIGINT,
  type STRING,
  tags MAP<STRING,STRING>,
  lat DECIMAL(9,7),
  lon DECIMAL(10,7),
  nds ARRAY<STRUCT<ref: BIGINT>>,
  members ARRAY<STRUCT<type: STRING, ref: BIGINT, role: STRING>>,
  changeset BIGINT,
  timestamp TIMESTAMP,
  uid BIGINT,
  user STRING,
  version BIGINT
)
STORED AS ORCFILE
LOCATION 's3://osm-pds/planet/';

# Test Query

Select * from planet LIMIT 100;

# Locational Query

SELECT * from planet
WHERE type = 'node'
  AND tags['amenity'] IN ('veterinary')
  AND lat BETWEEN -27.8 AND -27.3
  AND lon BETWEEN 152.2 AND 153.5;
```