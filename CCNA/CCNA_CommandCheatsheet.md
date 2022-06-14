# CCNA
## 1. Static Routes
![](/CCNA/Images/StaticRoutes.PNG)
#### PC0 Config
Just IP configuration for PC1-192.168.1.1 and Gateway_IP-192.168.1.

#### R1 Config

```sh
R1(config)#interface g0/0
R1(config-if)#ip address 192.168.1.254 255.255.255.0
R1(config-if)#description **to SW0**
R1(config-if)#interface g0/1
R1(config-if)#ip address 192.168.12.1 255.255.255.0
R1(config-if)#description **to R2**
R1(config)#ip route 192.168.3.0 255.255.255.0 192.168.12.2
```
#### R2 Config

```sh
R2(config)#interface g0/0
R2(config-if)#ip address 192.168.12.2 255.255.255.0
R2(config-if)#description **to R1**
R2(config-if)#interface g0/1
R2(config-if)#ip address 192.168.13.1 255.255.255.0
R2(config-if)#description **to R3**
R2(config)#ip route 192.168.1.0 255.255.255.0 192.168.12.1
R2(config)#ip route 192.168.3.0 255.255.255.0 192.168.13.2
```

#### R3 Config

```sh
R3(config)#interface g0/0
R3(config-if)#ip address 192.168.13.2 255.255.255.0
R3(config-if)#description **to R2**
R3(config-if)#interface g0/1
R3(config-if)#ip address 192.168.3.254 255.255.255.0
R3(config-if)#description **to SW1**
R3(config)#ip route 192.168.1.0 255.255.255.0 192.168.13.1
```

#### PC1 Config
Just IP configuration for PC1-192.168.3.1 and Gateway_IP-192.168.3.254

## 2. VLANs

![](/CCNA/Images/VLANs.PNG)
#### PC1 Config
PC1 config is just IP-Config: 10.0.0.1/26 and Gateway-IP: 10.0.0.62
#### PC2 Config
PC2 config is just IP-Config: 10.0.0.2/26 and Gateway-IP: 10.0.0.62
#### PC3 Config
PC3 config is just IP-Config: 10.0.0.65/26 and Gateway-IP: 10.0.0.126
#### PC4 Config
PC4 config is just IP-Config: 10.0.0.66/26 and Gateway-IP: 10.0.0.126
#### PC5 Config
PC5 config is just IP-Config: 10.0.0.129/26 and Gateway-IP: 10.0.0.190
#### PC6 Config
PC6 config is just IP-Config: 10.0.0.130/26 and Gateway-IP: 10.0.0.190
#### SW1 Config
```sh
SW1(config)# interface range g0/1,f3/1,f4/1
SW1(config-if-range)# switchport mode access
SW1(config-if-range)# switchport access vlan 10
SW1(config-if-range)# interface range g1/1,f5/1,f6/1
SW1(config-if-range)# switchport mode access
SW1(config-if-range)# switchport access vlan 20
SW1(config-if-range)# interface range g2/1,f7/1,f8/1
SW1(config-if-range)# switchport mode access
SW1(config-if-range)# switchport access vlan 30
SW1(config-if-range)# vlan 10
SW1(config-vlan)# name ENGINEERING
SW1(config-vlan)# vlan 20
SW1(config-vlan)# name HR
SW1(config-vlan)# vlan 30
SW1(config-vlan)# name SALES
```
#### R1 Config
```sh
R1(config)# interface g0/0
R1(config-if)# ip address 10.0.0.62 255.255.255.192
R1(config-ig)# no shutdown
R1(config-if)# interface g0/1
R1(config-if)# ip address 10.0.0.126 255.255.255.192
R1(config-ig)# no shutdown
R1(config-if)# interface g0/2
R1(config-if)# ip address 10.0.0.190 255.255.255.192
R1(config-ig)# no shutdown
```
## 3. Trunk Ports/ROAS
![](/CCNA/Images/TrunkPorts.PNG)
#### PC1 Config
PC1 config is just IP-Config: 10.0.0.1/26 and Gateway-IP: 10.0.0.62
#### PC2 Config
PC2 config is just IP-Config: 10.0.0.2/26 and Gateway-IP: 10.0.0.62
#### PC3 Config
PC3 config is just IP-Config: 10.0.0.129/26 and Gateway-IP: 10.0.0.190
#### PC4 Config
PC4 config is just IP-Config: 10.0.0.130/26 and Gateway-IP: 10.0.0.190
#### PC5 Config
PC5 config is just IP-Config: 10.0.0.65/26 and Gateway-IP: 10.0.0.126
#### PC6 Config
PC6 config is just IP-Config: 10.0.0.4/26 and Gateway-IP: 10.0.0.62
#### PC7 Config
PC7 config is just IP-Config: 10.0.0.3/26 and Gateway-IP: 10.0.0.62
#### SW1 Config
```sh
SW1(config)# interface range f0/1-2
SW1(config-if-range)# switchport mode access
SW1(config-if-range)# switchport access vlan 10
SW1(config)# interface range f0/3-4
SW1(config-if-range)# switchport mode access
SW1(config-if-range)# switchport access vlan 30
SW1(config-if-range)# interface g0/1
SW1(config-if)# switchport mode trunk
SW1(config-if)# switchport trunk allowed vlan 10,30
SW1(config-if)# switchport trunk native vlan 1001
```
#### SW2 Config
```sh
SW2(config)# interface range f0/1
SW2(config-if-range)# switchport mode access
SW2(config-if-range)# switchport access vlan 20
SW2(config)# interface range f0/2-3
SW2(config-if-range)# switchport mode access
SW2(config-if-range)# switchport access vlan 10
SW2(config-if-range)# interface g0/1
SW2(config-if)# switchport mode trunk
SW2(config-if)# switchport trunk allowed vlan 10,30
SW2(config-if)# swithcport trunk native vlan 1001
SW2(config-if)# vlan 30
SW2(config-vlan)# exit
SW2(config)# interface g0/2
SW2(config-if)# switchport mode trunk
SW2(config-if)# switchport trunk allowed vlan 10,20,30
SW2(config-if)# swithchport trunk native clan 1001
```
#### R1 Config
```sh
R1(config)# interface g0/0
R1(config-if)# no shutdown
R1(config-if)# interface g0/0.10
R1(config-subif)# encapsulation dot1q 10
R1(config-subif)# ip address 10.0.0.62 255.255.255.192
R1(config-if)# interface g0/0.20
R1(config-subif)# encapsulation dot1q 20
R1(config-subif)# ip address 10.0.0.126 255.255.255.192
R1(config-if)# interface g0/0.30
R1(config-subif)# encapsulation dot1q 30
R1(config-subif)# ip address 10.0.0.190 255.255.255.192
```
## 4. Layer 3 Switch

![](/CCNA/Images/Layer3_Switch.PNG)
#### PC1 Config
PC1 config is just IP-Config: 10.0.0.1/26 and Gateway-IP: 10.0.0.62
#### PC2 Config
PC2 config is just IP-Config: 10.0.0.2/26 and Gateway-IP: 10.0.0.62
#### PC3 Config
PC3 config is just IP-Config: 10.0.0.129/26 and Gateway-IP: 10.0.0.190
#### PC4 Config
PC4 config is just IP-Config: 10.0.0.130/26 and Gateway-IP: 10.0.0.190
#### PC5 Config
PC5 config is just IP-Config: 10.0.0.65/26 and Gateway-IP: 10.0.0.126
#### PC6 Config
PC6 config is just IP-Config: 10.0.0.4/26 and Gateway-IP: 10.0.0.62
#### PC7 Config
PC7 config is just IP-Config: 10.0.0.3/26 and Gateway-IP: 10.0.0.62
#### SW1 Config
```sh
SW1(config)# interface range f0/1-2
SW1(config-if-range)# switchport mode access
SW1(config-if-range)# switchport access vlan 10
SW1(config)# interface range f0/3-4
SW1(config-if-range)# switchport mode access
SW1(config-if-range)# switchport access vlan 30
SW1(config-if-range)# interface g0/1
SW1(config-if)# switchport mode trunk
SW1(config-if)# switchport trunk allowed vlan 10,30
SW1(config-if)# switchport trunk native vlan 1001
```
#### SW2 Config
```sh
SW2(config)# interface range g1/0/3
SW2(config-if-range)# switchport mode access
SW2(config-if-range)# switchport access vlan 20
SW2(config)# interface range f1/0/4-5
SW2(config-if-range)# switchport mode access
SW2(config-if-range)# switchport access vlan 10
SW2(config-if-range)# interface g1/0/1
SW2(config-if)# switchport mode trunk
SW2(config-if)# switchport trunk allowed vlan 10,30
SW2(config-if)# swithcport trunk native vlan 1001
SW2(config-if)# vlan 30
SW2(config-vlan)# exit
SW2(config)# interface g1/0/2
SW2(config-if)# no switchport
SW2(config-if)# ip address 10.0.0.193 255.255.255.252
SW2(config-if)# exit
SW2(config)# ip routing
SW2(config)# ip route 0.0.0.0 0.0.0.0 10.0.0.194
SW2(config)# interface vlan 10
SW2(config-if)# ip address 10.0.0.62 255.255.255.192
SW2(config-if)# no shutdown
SW2(config-if)# interface vlan 20
SW2(config-if)# ip address 10.0.0.126 255.255.255.192
SW2(config-if)# no shutdown
SW2(config-if)# interface vlan 30
SW2(config-if)# ip address 10.0.0.190 255.255.255.192
SW2(config-if)# no shutdown
```
#### R1 Config
```sh
R1(config)# ip route 10.0.0.0 255.255.255.192 10.0.0.193 
R1(config)# ip route 10.0.0.128 255.255.255.192 10.0.0.193 
R1(config)# ip route 10.0.0.64 255.255.255.192 10.0.0.193 
R1(config)# interface g0/0
R1(config-if)# ip address 10.0.0.194 255.255.255.252
```
## 5. Spanning Tree Protocol Comprehension

![](/CCNA/Images/STP_Comp.PNG)

| Bridge ID (62 bits) |
|---|
| Bridge Priority (16 bits) + MAC Address (48 bits) |

| Bridge Priority (16 bits) |
|---|
| Bridge Priority (4 bits) + Extended System ID/VLAN ID (12 bits) |                                                               

1. The first step is to know which switch is the root bridge. So following the process of designation the switch with the lowest Bridge ID will be the root bridge. Following that, SW3 will be the root bridge, so all the ports of the switch will be a designated port (forwarding state).
2. The second step is to know the root port (Forwarding State) of each remaining switch. The process to elect the root port is the following:
   - 1: Lowest root cost
   - 2: Lowest neighbor Bridge ID (Bridge Priority + MAC Address)
   - 3: Lowest neighbor Port ID (Port Priority + Port Number)
   Following the above.
3. Each remaining collisioin domain will select ONE interface to be a designated port (forwarding state). The other port in the collision domain will be non-designated (blocking). Designated port selection:
   - 1: Interface on switch with lowest root cost
   - 2: Interface on switch with lowest Bridge ID
   
#### SW1 Port State
 - F0/1: Non-Designated Port
 - F0/2: Non-Designated Port
 - F0/3: Non-Designated Port
 - F0/4: Root Port

#### SW2 Port State
 - F0/1: Designated Port
 - F0/2: Designated Port
 - F0/3: Non-Designated Port
 - G0/1: Root Port
 
#### SW3 Port State (Root Bridge)
 - F0/1: Designated Port
 - F0/2: Designated Port
 - F0/3: Designated Port
 - G0/1: Designated Port

#### SW4 Port State
 - G0/1: Designated Port
 - G0/2: Root Port

## 6. Configuring STP (PVST+)
![](/CCNA/Images/STP_Configuring.PNG)

Spanning Tree runs by default, however there is no garanty the networks follows the optimal path. First of all, is to check the current STP topology, root bridge and port states using the command `SW1# show spanning-tree` on every switch.

#### 1. Configure SW1 as the primary root for VLAN 1 and the secondary root for VLAN 2. Configure SW2 and the primary root for VLAN 2 and the secondary root for VLAN 1. What is the STP role/state of each port on each switch now?
SW1:
```sh
SW1(config)# spanning-tree vlan 1 root primary
SW1(config)# spanning-tree vlan 2 root secondary
```

SW2:
```sh
SW2(config)# spanning-tree vlan 1 root secondary
SW2(config)# spanning-tree vlan 2 root primary
```
#### 2. Increase the VLAN 1 cost of SW4's F0/2 interface to 100. Does SW4 select a different root port? Why/Why not?
```sh
SW4(config)# interface f0/2
SW4(config-if)# spanning-tree vlan 1 cost 100
SW4(config-if)# do show spanning-tree vlan 1
```
#### 3. Increase the VLAN 1 port priority of SW1's F0/1 to 240. Does SW3 select a different root port? Why/Why not?
SW1:
```sh
SW1(config)# interfaces f0/1
SW1(config-if)# spanning-tree vlan 1 port-priority 240
```

#### 4. Configure PortFast and BPDU Guard on the F0/3 interfaces of SW3/SW4.

SW3:
```sh
SW3(config)# interface f0/3
SW3(config-if)# spanning-tree portfast
SW3(config-if)# spanning-tree bpdguard enable
```

SW4:
```sh
SW4(config)# interface f0/3
SW4(config-if)# spanning-tree portfast
SW4(config-if)# spanning-tree bpdguard enable
```

## 7. EtherChannel

![](/CCNA/Images/EtherChannel.PNG)
#### PC1 Configuration
PC1 config is just IP-Config: 172.16.1.1/24 and Gateway-IP: 172.16.1.254/24

#### PC2 Configuration
PC2 config is just IP-Config: 172.16.1.2/24 and Gateway-IP: 172.16.1.254/24

#### SRV1 Configuration
SRV1 config is just IP-Config: 172.16.2.1/24 and Gateway-IP: 172.16.2.254/24

#### ASW1 Configuration
Layer 2 EtherChannel LACP Configuration to DSW1
```sh
ASW1(config)# interface range g0/1-2
ASW1(config-if-range)# channel-group 1 mode active
ASW1(config-if-range)# interface po1
ASW1(config-if)# switchport mode trunk
```

Load-Balance based on source and destination IP
```sh
ASW1(config)# port-channel load-balance src-dst-ip
```

#### ASW2 Configuration
Layer 2 EtherChannel PAgP Configuration to DSW2
```sh
ASW2(config)# interface range g0/1-2
ASW2config-if-range)# channel-group 1 mode active
ASW2(config-if-range)# interface po1
ASW2(config-if)# switchport mode trunk
```
Load-Balance based on source and destination IP
```sh
ASW2(config)# port-channel load-balance src-dst-ip
```

#### DSW1 Configuration
Layer 2 EtherChannel LACP Configuration to ASW1
```sh
DSW1(config)# interface range g1/0/3-4
DSW1(config-if-range)# channel group 1 mode active
DSW1(config-if-range)# interface po1
DSW1(config-if)# switchport trunk encapsulation dot1q
DSW1(config-if)# switchport mode trunk
```

Layer 3 EtherChannel Static EtherChannel to DSW2
```sh
DSW1(config-if)# interface range g1/0/1 - 2
DSW1(config-if-range)# no switchport
DSW1(config-if-range)# channel-group 2 mode on
DSW1(config-if-range)# interface po2
DSW1(config-if)# ip address 10.0.0.1 255.255.255.252
```
Static Routing between VLANs
```sh
DSW1(config)# ip routing
DSW1(config)# ip route 172.16.2.0 255.255.255.0 10.0.0.2
```

Load-Balance based on source and destination IP
```sh
DSW1(config)# port-channel load-balance src-dst-ip
```

#### DSW2 Configuration
Layer 2 EtherChannel PAgP Confiugration to ASW2
```sh
DSW2(config)# interface range g1/0/3-4
DSW2(config-if-range)# channel group 1 mode active
DSW2(config-if-range)# interface po1
DSW2(config-if)# switchport trunk encapsulation dot1q
DSW2(config-if)# switchport mode trunk
```

Layer 3 EtherChannel Static EtherChannel to DSW1
```sh
DSW2(config-if)# interface range g1/0/1 - 2
DSW2(config-if-range)# no switchport
DSW2(config-if-range)# channel-group 2 mode on
DSW2(config-if-range)# interface po2
DSW2(config-if)# ip address 10.0.0.2 255.255.255.252
```

Static Routing between VLANs
```sh
DSW2(config)# ip routing
DSW2(config)# ip route 172.16.1.0 255.255.255.0 10.0.0.1
```
Load-Balance based on source and destination IP
```sh
DSW2(config)# port-channel load-balance src-dst-ip
```
## 8. Floating Static Routes
![](/CCNA/Images/FloatingStaticRoutes.PNG)

#### 1. Check the routing tables of R1 and R2. Which dynamic routing protocol is Enterprise A using? Which route will be used if PC1 tries to access SRV1? Which route will be used if PC1 tries to access remote server 1.1.1.1 over the Internet?

To check the routing tables `R1# show ip route`. Enterprise A is using OSPF. The that will be used is the OSPF route `10.0.2.0/24 [110/2] via 10.0.0.2, 00:28:43, GigabitEthernet0/2/0`. The route to access 1.1.1.1 is `0.0.0.0/0 [1/0] via 203.0.113.9`.

#### 2. Configure floating static routes on R1 and R2 that allow PC1 to reach SRV1 if the link between R1 and R2 fails. Do the routes enter the routing tables of R1 and R2?

As we want the OSPF route working by default, we have to set the static routes on R1 and R2 with a higher administrative distance, in order to static routes works as backup route. This routes won't enter into the routing table cause they aren't in use and works as backups routes.

###### R1 Configuration
```sh
R1(config)# ip route 10.0.2.0 255.255.255.0 203.0.113.1 111
```
###### R2 Configuration
```sh
R2(config)# ip route 10.0.1.0 255.255.255.0 203.0.113.5 111
```

#### 3. Shut down the G0/2/0 interface of R1 or R2. Do the floating static routes enter the routing tables of R1 and R2? Ping from PC1 to SRV1 to confirm.
     
Yes, as the OSPF routes are no more available the static routes that we configured now works as by default.

## 9. EIGRP (Enhanced Interior Gateway Routing Protocol)
![](/CCNA/Images/EIGRP.PNG)

#### 1. Configure the appropriate hostnames and IP addresses on each device. Enable router interfaces.
On every router this are the following commands to run replacing it with the appropiate interface and ip/mask:
```sh
R1(config)# interface g0/0
R1(config-if)# ip address 192.168.4.254 255.255.255.0
R1(config-if)# no shutdown
```

#### 2. Configure a loopback interface on each router (1.1.1.1/32 for R1, 2.2.2.2/32 for R2, etc.)
On every router this are the following commands to run, replacing it with the appropiate ip address of the loopback.
```sh
R1(config)# interface l 0
R1(config)# ip address 1.1.1.1 255.255.255.255
```
#### 3. Configure EIGRP on each router. Disable auto-summary. Enable EIGRP on each interface (including loopback interfaces). Configure passive interfaces where appropriate (including loopback interfaces).

##### R4 Configuration
```sh
R4(config-if)# router eigrp 100
R4(config-router)# network 10.0.34.0 0.0.0.3
R4(config-router)# network 10.0.24.0 0.0.0.3
R4(config-router)# network 4.4.4.4 0.0.0.0
R4(config-router)# no auto-summary
R4(config-router)# passive-interface l0
R4(config-router)# passive-interface g0/0
```
##### R3 Configuration
```sh
R3(config-if)# router eigrp 100
R3(config-router)# network 10.0.34.0 0.0.0.3
R3(config-router)# network 10.0.13.0 0.0.0.3
R3(config-router)# network 3.3.3.3 0.0.0.0
R3(config-router)# no auto-summary
R3(config-router)# passive-interface l0
```
##### R2 Configuration
```sh
R2(config-if)# router eigrp 100
R2(config-router)# network 10.0.12.0 0.0.0.3
R2(config-router)# network 10.0.24.0 0.0.0.3
R2(config-router)# network 2.2.2.2 0.0.0.0
R2(config-router)# no auto-summary
R2(config-router)# passive-interface l0
```
##### R1 Configuration
```sh
R1(config-if)# router eigrp 100
R1(config-router)# network 10.0.12.0 0.0.0.3
R1(config-router)# network 10.0.13.0 0.0.0.3
R1(config-router)# network 1.1.1.1 0.0.0.0
R1(config-router)# no auto-summary
R1(config-router)# passive-interface l0
```

#### 4. Configure R1 to perform unequal-cost load-balancing when sending network traffic to 192.168.4.0/24

##### R1 Configuration
```sh
R1(config-router)# variance 2
```

## 10. OSPF Part 1 (Open Shortest Path First)
![](/CCNA/Images/OSPF_1.PNG)

#### 1. Configure the appropriate hostnames and IP addresses on each device.  Enable router interfaces. (You don't have to configure ISPR1)
On every router this are the following commands to run replacing it with the appropiate interface and ip/mask:
```sh
R1(config)# interface g0/0
R1(config-if)# ip address 10.0.12.1 255.255.255.252
R1(config-if)# no shutdown
```
#### 2. Configure a loopback interface on each router (1.1.1.1/32 for R1, 2.2.2.2/32 for R2, etc.)
On every router this are the following commands to run, replacing it with the appropiate ip address of the loopback.
```sh
R1(config)# interface l0
R1(config)# ip address 1.1.1.1 255.255.255.255
```
#### 3. Configure OSPF on each router. Enable OSPF on each interface (including loopback interfaces). (Do not enable OSPF on R1's Internet link) Configure passive interfaces where appropriate (including loopback interfaces).

#### R1 Configuration
```sh
R1(config)# router ospf 1
R1(config-router)# network 10.0.13.1 0.0.0.0 area 0
R1(config-router)# network 10.0.12.1 0.0.0.0 area 0
R1(config-router)# network 1.1.1.1 0.0.0.0 area 0
R1(config-router)# passive-interface l0
```
#### R2 Configuration
```sh
R2(config)# router ospf 2
R2(config-router)# network 10.0.24.1 0.0.0.0 area 0
R2(config-router)# network 10.0.12.2 0.0.0.0 area 0
R2(config-router)# network 2.2.2.2 0.0.0.0 area 0
R2(config-router)# passive-interface l0
```
#### R3 Configuration
```sh
R3(config)# router ospf 3
R3(config-router)# network 10.0.13.2 0.0.0.0 area 0
R3(config-router)# network 10.0.34.1 0.0.0.0 area 0
R3(config-router)# network 3.3.3.3 0.0.0.0 area 0
R3(config-router)# passive-interface l0
```
#### R4 Configuration
```sh
R4(config)# router ospf 4
R4(config-router)# network 0.0.0.0 255.255.255.255 area 0
R4(config-router)# passive-interface g0/0
R4(config-router)# passive-interface l0
```

#### 4. Configure R1 as an ASBR that advertises a default route in to the OSPF domain.
```sh
R1(config-router)# default-information originate
R1(config-router)# exit
R1(config)# ip route 0.0.0.0 0.0.0.0 203.0.113.2
```
#### 5. Check the routing tables of R2, R3, and R4.  What default route(s) were added?
In order to see ospf database `R1# show ip ospf database`.

## 11. OSPF Part 2
#### OSPF Cost
A command to see the OSPF configuration: `R1# show ip ospf interface brief`
There are three ways to modify the OSPF cost:
   1. Change the reference bandwidth: `R1(config-router)# auto-cost reference-bandwith megabits-per-second`
   2. Manual configuration: `R1(config-if)# ip ospf cost cost`
   3. Change the interface bandwidth (not recommended): `R1(config-if)# bandwidth kilobits-per-second`
The best way is to change the reference bandwidth to a value greater than the fastest links in the network.

##### OSPF Neighbors
OSPF neighbors is the main task in configuring OSPF, once routers become neighbors, they automatically do the work of sharing network, calculating routes, etc. 

When OSPF is activated on an interface, the router starts sending OSPF hello messages out of the inerface at regular intervals(determined by the hello timer). These are used to introduce the router to potential OSPF neighbors.

![OSPF_Neighbors](https://user-images.githubusercontent.com/49905811/172799195-23649d70-9ea2-409a-b16c-5263ac65905b.PNG)

| Type | Name | Purpose |
| :-: | :-: | :-: |
| 1 | **Hello** | Neighbor discovery and maintenance |
| 2 | **Database Description (DBD)** | Summary of the LSDB of the router. Used to check if the LSDB of each router is the same |
| 3 | **Link-State Request (LSR)** | Request specific LSAs from the neighbor |
| 4 | **Link-State Update (LSU)** | Sends specific LSAs to the neighbor |
| 5 | **Link-State Acknowledgement (LSAck)** | Used to acknowledge that the router received a message |

![](/CCNA/Images/OSPF_1.PNG)

#### 1. Configure the appropriate hostnames and IP addresses on each device.  Enable router interfaces. (You don't have to configure ISPR1)
On every router this are the following commands to run replacing it with the appropiate interface and ip/mask:
```sh
R1(config)# interface g0/0
R1(config-if)# ip address 10.0.12.1 255.255.255.252
R1(config-if)# no shutdown
```
#### 2. Configure a loopback interface on each router (1.1.1.1/32 for R1, 2.2.2.2/32 for R2, etc.)
On every router this are the following commands to run, replacing it with the appropiate ip address of the loopback.
```sh
R1(config)# interface l0
R1(config)# ip address 1.1.1.1 255.255.255.255
```
#### 3. Enable OSPF directly on each interface of the routers. Configure passive interfaces as appropriate.
##### R1 Configuration
```sh
R1(config)# router ospf 1
R1(config-router)# network 10.0.13.1 0.0.0.0 area 0
R1(config-router)# network 10.0.12.1 0.0.0.0 area 0
R1(config-router)# network 1.1.1.1 0.0.0.0 area 0
R1(config-router)# passive-interface l0
```
##### R2 Configuration
```sh
R2(config)# router ospf 2
R2(config-router)# network 10.0.24.1 0.0.0.0 area 0
R2(config-router)# network 10.0.12.2 0.0.0.0 area 0
R2(config-router)# network 2.2.2.2 0.0.0.0 area 0
R2(config-router)# passive-interface l0
```
##### R3 Configuration
```sh
R3(config)# router ospf 3
R3(config-router)# network 10.0.13.2 0.0.0.0 area 0
R3(config-router)# network 10.0.34.1 0.0.0.0 area 0
R3(config-router)# network 3.3.3.3 0.0.0.0 area 0
R3(config-router)# passive-interface l0
```
##### R4 Configuration
```sh
R4(config)# router ospf 4
R4(config-router)# network 0.0.0.0 255.255.255.255 area 0
R4(config-router)# passive-interface g0/0
R4(config-router)# passive-interface l0
```

#### 4. Configure the reference bandwidth on each router so a FastEthernet interface has a cost of 100.
##### R1 Configuratio
`sh
R1(config-router)# auto-cost reference-bandwidth 10000
`
##### R2 Configuration
`sh
R2(config-router)# auto-cost reference-bandwidth 10000
`
##### R3 Configuration
`sh
R3(config-router)# auto-cost reference-bandwidth 10000
`
##### R4 Configuration
`sh
R4(config-router)# auto-cost reference-bandwidth 10000
`

#### 5. Configure R1 as an ASBR that advertises a default route in to the OSPF domain.

##### R1 Configuration
`sh
R1(config-router)# default-information originate
R1(config-router)# exit
R1(config)# ip route 0.0.0.0 0.0.0.0 203.0.113.2
`
#### 6. Check the routing tables of R4. What default route(s) were added?
On R4 both routes via R2 and R3 instead of the less cost via R2, that's because OSPF external cost takes part in and it decides the internal cost is redundant. Otherwise this is a CCNP topic.

## 12. OSPF Part 3
#### OSPF Nertwork Types
The OSPF 'network type' refers to the type of connection between OSPF neighbors. There are three main OSPF network types:
   - Broadcast: Enabled by default on Ethernet and FDDI(Fiber Distributed Data Interfaces) interfaces
   - Point-to-point: Enabled by default on PPP(Point-to-Point Protocol) and HDLC(High-Level Data Link Control) interfaces
   - Non-Broadcast: Enabled by default on Frame Relay and X.25 interfaces

**Broadcast:**

![OSPF_BroadcastNetworkType](https://user-images.githubusercontent.com/49905811/173338503-9386fae9-ccb4-4915-9ed1-1f86dfd47e68.PNG)

Enabled on Ethernet and FDDI interfaces by default. Routers dynamically discover neighbors by sending/listening for OSPF Hello messages using multicast address 224.0.0.5.

A DR (Designated Router) and BDR (Backup Designated Router) must be elected on each subnet (only DR if there are no OSPF neighbors). Routers which aren't the DR or BDR become a DROther.

The DR/BDR election order of priority:
   1. Highest OSPF interface priority
   2. Highest OSPF Router ID
'First place' becomes the DR fot he subnet, 'second place' becomes the BDR. The default OSPF interface priority is 1 on all interfaces. In the broadcast network type, routers will only form a full OSPF adjacency with the DR and BDR of the segment.

Therefore, routers only exchange LSAs with the DR and BDR. DROthers will not exchange LSAs with each other. All routers will still have the same LSDB, but this reduces the amount of LSAs flooding the network.

**Point-to-point:**
![Poin-to-Point](https://user-images.githubusercontent.com/49905811/173549811-99e779d2-b020-4b00-a91a-20bd9a9f416e.PNG)

Enabled on serial interfaces using the PPP or HDLC encapsulations by default. Routers dynamically disover neighbors by sending/listening for OSPF Hello messages using multicast address 224.0.0.5. A DR and BDR are not elected. These encapsulation are used for 'point-to-point' connections.

Therefore there is no pint in electing a DR and BDR. The two routers will form a Full adjacency with each other.

###### Serial Interfaces
One side of a serial connection functions as DCE (Data Communications Equipment). The other side functions as DTE (Data Terminal Equipment). The DCE side needs to specify the clock rate (speed) of the connection.

The default encapsulation on a serial interface is HDLC. If you change the encapsulation, it must match on both ends or the interface will go down.

- It can be configured PPP encapsulation with this command: `R1(config-if)# encapsultaion ppp`
- Identify which is DCE/DTE: `R1# show controllers *interface-id*`
- Must configure the clock rate on the DCE side: `R1(config-if)# clock rate *bits-per-second*`

It can be configured the OSPF network type on an interface with ip ospf network *type*. For example, if two routers are directly connected with an Ethernet link, ther is no need for a DR/BDR. You can configure the point-to-point network type in this case.

Note: No all network types work on all link types (for example, a serial link cannot use the broadcast network type)

|**Broadcast**|**Point-to-Point**|
|-|-|
|Default on Ethernet, FDDI interfaces|Default on HDLC, PP(serial) interfaces|
|DR/DBR elected| No DR/BDR|
|Neighbors dynamically discovered|Neighbors dynamically discovered|
|Default timers: Hello 10, Dead 40| Default timers: Hello 10, Dead 40|
(Non-broadcast network type default timers = Hello 30, Dead 120)

#### OSPF Neighbor/Adjacency Requirements
1. Area nmber must match
2. Interfaces must be in the same subnet
3. OSPF process must not be shutdown
4. OSPF Router IDs must be unique
5. Hello adn Dead timers must match
6. Authentication settings must match
7. IP MTU settings must match   ||
8. OSPF Network Type must match || (Can become OSPF neighbors, but OSPF doesn't operate properly)

#### OSPF LSA Types
![LSA_Types](https://user-images.githubusercontent.com/49905811/173555847-85b8cfc2-7df7-4edf-a06f-d669920da4fd.PNG)

The OSPF LSDB is made up of LSAs. There are 11 types of LSA, but there are only 3 should be aware of for the CCNA:
- Type 1 (Router LSA):
   - Every OSPF router generates this type of LSA.
   - It identifies the router using its router ID.
   - It also lists networks attached to the router's OSPF-activated interfaces.
- Type 2 (Network LSA)
   - Generated by the DR of each 'multi-access' network (ie. the broadcast network type).
   - Lists the routers which are attached to the multi-access network.
- Type 5 (AS External LSA)
   - Generated by ASBRs to describe routes to destinations outside of the AS (OSPF domain).
