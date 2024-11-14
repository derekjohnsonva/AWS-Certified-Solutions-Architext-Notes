Key terms
Direct attached storage - storage on the EC2 host
	Can be risky but is faster
Network attached storage - volumes delivered over network
	More reliable
Ephemeral Storage - temporary
Persistent - permanent long term storage. Lives past EC2 instance
Block storage - volume presented to the OS. No structure provided. Mountable and bootable.
File Storage - Presented as a file structure. Not bootable. Is mountable
Object storage - collection of objects. Not mountable, not bootable.

**Performance Metrics**
IO Block Size = size of blocks of data written to disk
IOPS = Blocks per second
Throughput = (IOPS) x (IO Block Size)

