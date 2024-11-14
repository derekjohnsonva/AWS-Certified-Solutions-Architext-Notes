Classless Inter-Domain Routing (CIDR) allows network routers to route data packets to the respective device based on the indicated subnet. Instead of classifying the IP address based on classes, routers retrieve the network and host address as specified by the CIDR suffix.

The suffix (i.e. the /x part) tells us how big the range is. Each increment in the suffix increases the range by a factor of 2. Thus, two /17 ranges can fit into one /16

Ex: 172.31.0.0/16

https://aws.amazon.com/what-is/cidr/