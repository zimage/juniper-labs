# Day One: Configuring Segment Routing with Junos

I implemented the router topology from the Juniper publication
"Day One: Configuring Segment Routing with Junos" using logical
systems on an ACX2100 for the provider routers and an ACX1100
for the customer routers.Both ACX routers are running JunOS 20.3R1.8.

provider-c123.conf has the config for the provider routers that matches
the topology described at the end of chapter 1 and has all the
additional config from chapters 2 and 3. 

## Physical Connections
* ACX does not support using logical tunnel interfaces to connect logical systems, so a physical connection had to be used. A patch cable needs to be connected between ge-1/0/0 and ge-1/0/1. All of the inter-router links run accross this link.
* There is an L2VPN configured across the provider network. CE routers should connect to ge-1/1/0 and ge-1/1/1.
* There is an L3VPN configured across the provider network. CE3 connects to ge-1/1/2.3 and CE4 connects to ge-1/1/2.4

## Caveats
### Chapter 2
* `protocols mpls label-range static-label-range` doesn't seem to work on ACX, so I wasn't able to configure the adjacency sets.
* I did not configure the aggregated ethernet connection between R5 and R7. As such, I wasn't able to do the configuration in the "Label Per Member Link on Aggregated Ethernet" section

### Chapter 3
* ACX does not seem to support static srgb ranges, so the node indexes for IPv4 are 80040*x* instead of 1040*x* and for IPv6 are 80060*x* instead of 1060*x* where *x* is the router number
