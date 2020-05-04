# Static Routing 靜態路由

main part:

IP Routing CLI 

Static Routes Config 

Default Route Config & Individual Host Route 

IP Classless Routing 

Basic Output Interfaces & Next-Hop Router 

LB using Stactic Route 

-----------------------------------------------------------------------

* IEEE 802.1D Spanning Tree to avoid loop

Per-VLAN Spanning Tree (PVST+)—PVST+ is a Cisco enhancement of STP that provides a separate 802.1D spanning-tree instance for each VLAN configured in the network. ... The Cisco implementation of MSTP is often referred to as Multiple Spanning Tree (MST).

* IEEE 802.1Q Trunking Protocol to save the port

VLAN Trunking Protocol (VTP) is a Cisco proprietary protocol that propagates the definition of Virtual Local Area Networks (VLAN) on the whole local area network. To do this, VTP carries VLAN information to all the switches in a VTP domain. VTP advertisements can be sent over 802.1Q, and ISL (Inter-SW-Link) trunks.

* ISL, Inter-Switch Link (Trunking)

see IEEE 802.1Q

* ISR, Intergrated-Service Router

ISR stands for Integrated Service Router. The term “integrated services” describes a type of network architecture used to guarantee network Quality of Service (QoS). ISR series routers have edge networking capabilities and provide reliable, secure branch office connectivity.

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
        
        
* VLAN
        
 (1)
![1](https://scontent.ftpe8-2.fna.fbcdn.net/v/t1.0-9/95329352_4252055654808210_8847947893244428288_o.jpg?_nc_cat=103&_nc_sid=110474&_nc_ohc=x2YO4D6IHQEAX9EVNE9&_nc_ht=scontent.ftpe8-2.fna&oh=ae1aa732db78f5734c0486db6eee4f56&oe=5ED383DB)

 (2)
![2](https://scontent.ftpe8-3.fna.fbcdn.net/v/t1.0-9/95603496_4252055648141544_7257275771276754944_n.jpg?_nc_cat=106&_nc_sid=110474&_nc_ohc=EDmHEDonsFUAX8yi0Hy&_nc_ht=scontent.ftpe8-3.fna&oh=66a9de50df41775f605e5694d157a2ed&oe=5ED34C8A)

 (3)
![3](https://scontent.ftpe8-4.fna.fbcdn.net/v/t1.0-9/95592029_4252055751474867_3523580062852972544_n.jpg?_nc_cat=110&_nc_sid=110474&_nc_ohc=u_j36mgMAfcAX_IBeRv&_nc_ht=scontent.ftpe8-4.fna&oh=130d771ebb775f29103233031860d8f1&oe=5ED22312)

 (4)
![4](https://scontent.ftpe8-2.fna.fbcdn.net/v/t1.0-9/95140085_4252055638141545_1447246830193606656_n.jpg?_nc_cat=100&_nc_sid=110474&_nc_ohc=CT0wgQ79NvAAX-PZARo&_nc_ht=scontent.ftpe8-2.fna&oh=5e4835819bf964a3c5d90dbf77694d50&oe=5ED4E763)

 (5)
![5-1](https://scontent.ftpe8-1.fna.fbcdn.net/v/t1.0-9/95234947_4252055631474879_6953632977997791232_n.jpg?_nc_cat=105&_nc_sid=110474&_nc_ohc=NSkNQ-q60UQAX9-n8ep&_nc_ht=scontent.ftpe8-1.fna&oh=1e8e44b8f1454fe1226be07e0fd2cfcb&oe=5ED48C32)

 (6)
![5-2](https://scontent.ftpe8-4.fna.fbcdn.net/v/t1.0-9/96142849_4252055728141536_9060304541081141248_o.png?_nc_cat=102&_nc_sid=110474&_nc_ohc=s6kMG_jBmDQAX9aaqlq&_nc_ht=scontent.ftpe8-4.fna&oh=dad2963ef17a2ea2d4e20f8119b5399b&oe=5ED4BAE3)

 (7)
![6](https://scontent.ftpe8-2.fna.fbcdn.net/v/t1.0-9/95215566_4252055891474853_2773282699677270016_n.jpg?_nc_cat=100&_nc_sid=110474&_nc_ohc=j5mNR-hOJiEAX9r4e2H&_nc_ht=scontent.ftpe8-2.fna&oh=e6910cccbf2c40691eacab50ccce9226&oe=5ED5642F)

 (8)
![7](https://scontent.ftpe8-4.fna.fbcdn.net/v/t1.0-9/94977487_4252055771474865_6273576991744589824_n.jpg?_nc_cat=102&_nc_sid=110474&_nc_ohc=PC1S9V-CZqIAX8_ewCh&_nc_ht=scontent.ftpe8-4.fna&oh=850c6bca854c2d85364e08743ce75d18&oe=5ED42B44)

(9)
![8](https://scontent.ftpe8-3.fna.fbcdn.net/v/t1.0-9/95376283_4252055731474869_2103592131661660160_o.jpg?_nc_cat=111&_nc_sid=110474&_nc_ohc=-41okVfyqukAX8wUa4x&_nc_ht=scontent.ftpe8-3.fna&oh=2bffc79d4da09f00fc4cc28252bff588&oe=5ED39DE0)

(10)
![8-2](https://scontent.ftpe8-3.fna.fbcdn.net/v/t1.0-9/95771754_4252055681474874_2285555782730645504_n.jpg?_nc_cat=106&_nc_sid=110474&_nc_ohc=_8LH2yFFZ3oAX9qDOs3&_nc_ht=scontent.ftpe8-3.fna&oh=27c23e9effc80959570678c375ad7f2e&oe=5ED3101D)

 * VLAN - LAN
 
 (1)
 ![1](https://scontent.ftpe8-1.fna.fbcdn.net/v/t1.0-9/96174618_4255935744420201_8777232253148200960_o.jpg?_nc_cat=108&_nc_sid=110474&_nc_ohc=XJ8hiHxwrU8AX8e42pM&_nc_ht=scontent.ftpe8-1.fna&oh=1753e8d841ad62bc0761aa204bb2e7e7&oe=5ED4B43E)
 
 (2)
 ![2](https://scontent.ftpe8-3.fna.fbcdn.net/v/t1.0-9/96220336_4255936254420150_9109655325924917248_o.png?_nc_cat=111&_nc_sid=110474&_nc_ohc=wVd50fTW4DEAX-7qxCT&_nc_ht=scontent.ftpe8-3.fna&oh=66a0826400ee3a8c8b969c67e57c3d84&oe=5ED51355)
 
 (3)
 ![3](https://scontent.ftpe8-1.fna.fbcdn.net/v/t1.0-9/95443899_4255936544420121_6744229833141649408_o.jpg?_nc_cat=105&_nc_sid=110474&_nc_ohc=pVqBH-W-6_AAX-r0xUu&_nc_ht=scontent.ftpe8-1.fna&oh=7405de41314ee05b4f87b2b5c3df786c&oe=5ED6CE0A)
 
 (4)
 ![4](https://scontent.ftpe8-3.fna.fbcdn.net/v/t1.0-9/95743673_4255937381086704_8457140052953137152_o.png?_nc_cat=107&_nc_sid=110474&_nc_ohc=3JKbwX_hix4AX9Jwxnf&_nc_ht=scontent.ftpe8-3.fna&oh=534e220651ec455cf9867d20b580ea78&oe=5ED69AFA)
 
 * WAN (ISR)
 
 (1)
 ![5](https://scontent.ftpe8-2.fna.fbcdn.net/v/t1.0-9/95384806_4255938054419970_7213246128790175744_o.jpg?_nc_cat=100&_nc_sid=110474&_nc_ohc=OdEFonzLd9YAX_Ywd6E&_nc_ht=scontent.ftpe8-2.fna&oh=ea1ceeca59db34f4606ad06369164397&oe=5ED4EA2E)
 
 (2)
 ![6](https://scontent.ftpe8-3.fna.fbcdn.net/v/t1.0-9/95384794_4255938444419931_6214854987692900352_o.png?_nc_cat=106&_nc_sid=110474&_nc_ohc=FCjks0M7FRcAX-Ssqeq&_nc_ht=scontent.ftpe8-3.fna&oh=37ab58396a157b5d85005bd97964bff3&oe=5ED4B0D8)
 
 (3)
 ![7](https://scontent.ftpe8-2.fna.fbcdn.net/v/t1.0-9/95448336_4255938727753236_9045952340925874176_o.jpg?_nc_cat=103&_nc_sid=110474&_nc_ohc=fjpZZQyXqo8AX8eKRyM&_nc_ht=scontent.ftpe8-2.fna&oh=9e60ef3cc91ceb2327cd69bd85a69c6c&oe=5ED57732)
 
* ISR

(4)
![1](https://scontent.ftpe8-1.fna.fbcdn.net/v/t1.0-9/96091631_4255960481084394_8835927392179453952_o.jpg?_nc_cat=105&_nc_sid=110474&_nc_ohc=USTvw3mbtk8AX_2zuQy&_nc_ht=scontent.ftpe8-1.fna&oh=cbe4316a307b10bf298384b780b521ef&oe=5ED3A763)

(5)
![2](https://scontent.ftpe8-3.fna.fbcdn.net/v/t1.0-9/95846313_4255960947751014_1682300065202307072_o.png?_nc_cat=111&_nc_sid=110474&_nc_ohc=hJ8gVew6GaAAX8-j3ZA&_nc_ht=scontent.ftpe8-3.fna&oh=d5fedae620daaf5974c1978db99c2359&oe=5ED45563)

(6)
![3](https://scontent.ftpe8-2.fna.fbcdn.net/v/t1.0-9/95463983_4255961314417644_5500274989162561536_o.jpg?_nc_cat=103&_nc_sid=110474&_nc_ohc=YIDJW2eBXLIAX8EZK8X&_nc_ht=scontent.ftpe8-2.fna&oh=7d421dc22b01f42f088e13be31ef11c5&oe=5ED651F1)

(7)
![4](https://scontent.ftpe8-1.fna.fbcdn.net/v/t1.0-9/96084192_4255961677750941_7016745147295596544_o.png?_nc_cat=109&_nc_sid=110474&_nc_ohc=OdHZNHuJDKcAX_i5Sxj&_nc_ht=scontent.ftpe8-1.fna&oh=19004a18df2494e99cc8a8cca67b529a&oe=5ED5B689)


* LAN - VLAN

(1)
![5](https://scontent.ftpe8-3.fna.fbcdn.net/v/t1.0-9/95602690_4255962064417569_3783759870155554816_o.jpg?_nc_cat=106&_nc_sid=110474&_nc_ohc=5Hug6LjJbbkAX9XnNRP&_nc_ht=scontent.ftpe8-3.fna&oh=4def047b523029b3bf36d6fd432dd4a2&oe=5ED3E911)

(2)
![6](https://scontent.ftpe8-4.fna.fbcdn.net/v/t1.0-9/96215976_4255962427750866_6974268491968806912_o.png?_nc_cat=110&_nc_sid=110474&_nc_ohc=h01l2q4E_0sAX89Utd6&_nc_ht=scontent.ftpe8-4.fna&oh=ecae8ab472c84103cc8084c15b064149&oe=5ED5800D)

(3)
![7](https://scontent.ftpe8-4.fna.fbcdn.net/v/t1.0-9/96020537_4255963004417475_2689569114153811968_o.jpg?_nc_cat=104&_nc_sid=110474&_nc_ohc=CigFEVYuDCgAX8KW_wJ&_nc_ht=scontent.ftpe8-4.fna&oh=6bcd2caea27c48569b1ecdc0eadcecb4&oe=5ED6DF65)

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
