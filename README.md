# Static Routing 靜態路由

main part:

IP Routing CLI 

Static Routes Config 

Default Route Config & Individual Host Route 

IP Classless Routing 

Basic Output Interfaces & Next-Hop Router 

-----------------------------------------------------------------------

so on: 

LB using Stactic Route 

-----------------------------------------------------------------------
# IP Routing CLI

$no ip routing

$ip routing

R1$show interfaces ethernet 0

> Ethernet0 is up, line protocol is up

The hosts that are connected to segments interconnected with a single Router must have Routes pointing to the IP addr assigned on the router interfaces.


               --------------------
              |                    |
    HostA ----|                    |
              |                    |
              |                    |
    HostB ----|       Segment      |-default Route -> IP addr of Interface of Router
              |                    |
              |                    |
    HostC ----|                    |
              |                    |
               --------------------


For instance, all of the hosts on a segment can have a single Route pointing to IP addr of the Router's interface which is attached to the segment.

R2$show ip route

> 10.0.0.0/24 is subnetted, 2 subnets

> C 10.2.2.0 is directly connected. TokenRing0

> C 10.0.255.0 is directly connected. Serial1

-----------------------------------------------------------------------
# Static Route

to identify the network Prefixes of the networks that are Accessible thru other Routers. Then create Static Route for segements.

There are an important consideration is that host config, it then has entry point to the appropriate interface of the routers, then to create static routing on the closest router. Remember to config 2 sides to avoid errors.

        R2$ip route <remote IP addr> <subnetmask> <next hop Router>

-----------------------------------------------------------------------
# Default Route Config & Individual Host Route

for host route

however this ip addr is assigned for not only the host per se, can be addr of other router.

      h3$ip route <remote IP addr> <subnetmask> <next hop Router>

to check by

      h3$show ip route
      > then show routing table
      
      
Deafult Route:

                                               using ip classless
 
    Host ------ Segment ------- e0 - Router - s0 ------- Segemnt (Counterpart Router) 
       
 
 

      
for default route

      R0$ip route 0.0.0.0 0.0.0.0 <next hop router>
      R0$ip classless
 

to check by

      R0$debug ip packet
      R0$ping <ip addr>

-----------------------------------------------------------------------
# IP Classless Routing 

this cmd enable the Router to use classless algorithm to make routing decision.

          
                                    segment3
                                      |
                                      |
    Host ----- Segment1 --- e0-R-s0 ------ s0-R-e0 --------- Segment2 ----- Host

-----------------------------------------------------------------------
# Basic Output Interfaces & Next-Hop Router 

If a single router is used to perform routing among Segements that are directly attached to it, no extra routing config is required.

The router autoly places into routing table the network prefixes of the IP addresses from all the active (up both logical and physically) interfaces. 

       R1$show ip interfaces <interface id> <interface #> 
       >  Ethernet0 is up, line protocol is up.
       
if the above interface is assigned of 10.1.1.1 this ip addr, then we still can change it by cmd below, choosing one in the output of routing table.

       R1$show ip route
       > Routing Table of R1
       10.0.0.0/24. 3 subnets
       10.2.2.0
       10.1.1.0
       
to check active in both, or one up and anoter down

      R1$show interfaces ethernet 0
      Ethernet0 is up, line protocol is down
      
above status means that if that transceiver is disconnected from the hub, working not properly, then it turns to logically down. since Ethernet shall be always up phisically.
       10.0.255.0
