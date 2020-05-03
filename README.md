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

* IEEE 802.1D Spanning Tree 

Per-VLAN Spanning Tree (PVST+)—PVST+ is a Cisco enhancement of STP that provides a separate 802.1D spanning-tree instance for each VLAN configured in the network. ... The Cisco implementation of MSTP is often referred to as Multiple Spanning Tree (MST).

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
        
![1](https://scontent.ftpe8-2.fna.fbcdn.net/v/t1.0-9/95329352_4252055654808210_8847947893244428288_o.jpg?_nc_cat=103&_nc_sid=110474&_nc_ohc=x2YO4D6IHQEAX9EVNE9&_nc_ht=scontent.ftpe8-2.fna&oh=ae1aa732db78f5734c0486db6eee4f56&oe=5ED383DB)

![2](https://scontent.ftpe8-3.fna.fbcdn.net/v/t1.0-9/95603496_4252055648141544_7257275771276754944_n.jpg?_nc_cat=106&_nc_sid=110474&_nc_ohc=EDmHEDonsFUAX8yi0Hy&_nc_ht=scontent.ftpe8-3.fna&oh=66a9de50df41775f605e5694d157a2ed&oe=5ED34C8A)

![3](https://scontent.ftpe8-4.fna.fbcdn.net/v/t1.0-9/95592029_4252055751474867_3523580062852972544_n.jpg?_nc_cat=110&_nc_sid=110474&_nc_ohc=u_j36mgMAfcAX_IBeRv&_nc_ht=scontent.ftpe8-4.fna&oh=130d771ebb775f29103233031860d8f1&oe=5ED22312)

![4](https://scontent.ftpe8-2.fna.fbcdn.net/v/t1.0-9/95140085_4252055638141545_1447246830193606656_n.jpg?_nc_cat=100&_nc_sid=110474&_nc_ohc=CT0wgQ79NvAAX-PZARo&_nc_ht=scontent.ftpe8-2.fna&oh=5e4835819bf964a3c5d90dbf77694d50&oe=5ED4E763)

![5-1](https://scontent.ftpe8-1.fna.fbcdn.net/v/t1.0-9/95234947_4252055631474879_6953632977997791232_n.jpg?_nc_cat=105&_nc_sid=110474&_nc_ohc=NSkNQ-q60UQAX9-n8ep&_nc_ht=scontent.ftpe8-1.fna&oh=1e8e44b8f1454fe1226be07e0fd2cfcb&oe=5ED48C32)

![5-2](https://scontent.ftpe8-4.fna.fbcdn.net/v/t1.0-9/96142849_4252055728141536_9060304541081141248_o.png?_nc_cat=102&_nc_sid=110474&_nc_ohc=s6kMG_jBmDQAX9aaqlq&_nc_ht=scontent.ftpe8-4.fna&oh=dad2963ef17a2ea2d4e20f8119b5399b&oe=5ED4BAE3)

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
