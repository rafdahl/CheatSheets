initial
```
(config)# ip domain-name home.net
(config)# hostname SW01
(config)# interface Vlan1
(config)# description Management Vlan
(config)# ip address 192.168.100.200 255.255.255.0
```
Verify vtp
```
# show vtp status
# vtp transparent   [Options: client, server, transparent]
# vtp domain name
```
Configure access ports
```
(config)# interface Gi/0/1
(config-if)# description <DESCRIPTION>
(config-if)# switchport access vlan <vlan>
(config-if)# switchport mode access
(config-if)# no cdp enable
(config-if)# spanning-tree portfast
(config-if)# no shut
```

configure trunks
```
(config)# interface Gi0/1
(config-if)# description <DESCRIPTION>
(config-if)# switchport trunk encapsulation dot1q
(config-if)# switchport mode trunk
(config-if)# speed 1000
(config-if)# duplex full
```
Configure vty and console
```
(config)# line vty 0 4
(config-line)# transport input ssh
(config-line)# login local
(config-line)# password <password>
(config-line)# exit

(config)# line console 0
(config-line)# logging synchronous
(config-line)# login local
```

Configure ssh key
```
(config)# crypto key generate rsa modulus

The name for the keys will be: Switch01.routefreak.com
Choose the size of the key modulus in the range of 360 to 2048 for your

General Purpose Keys. Choosing a key modulus greater than 512 may take
a few minutes.

How many bits in the modulus [512]: 1024
 % Generating 1024 bit RSA keys, keys will be non-exportable...[OK]
```
Save the configuration
```
# copy running-config startup-config
```
