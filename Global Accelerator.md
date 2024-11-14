 An alternative to [[CloudFront]]
You start with 2 anycast IP addresses
	anycast IP allow a single IP to be in multiple locations. Routed to the closest location.

If a user connects to these anycast IPs, they will be routed to a Global Accelerator location on the public internet and from there their traffic will take place on the AWS global network
	This network is more optimized for speed.

How is this different from [[CloudFront]]???
CloudFront - Content Delivery Network
- ﻿﻿Improves performance for your cacheable content (such as images and videos)
- ﻿﻿Content is served at the edge
Global Accelerator
- ﻿﻿No caching, proxying packets at the edge to applications running in one or more AWS Regions.
- ﻿﻿Improves performance for a wide range of applications over TCP or UDP
- ﻿﻿Good for HTTP use cases that require static IP addresses
- ﻿﻿Good for HTTP use cases that required deterministic, fast regional failover