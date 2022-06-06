# CCNA
## 1. Static Routes
![](/CCNA/Images/StaticRoutes.PNG)
#### PC0 Config
Just IP configuration for PC1-192.168.1.1 and Gateway_IP-192.168.1.254
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
