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

#### R1 Config
