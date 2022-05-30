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
