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

