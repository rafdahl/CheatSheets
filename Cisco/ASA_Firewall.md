
GATHERING DATA TO MAKE A CHEATSHEET - - - IN PROGRESS


## ASA Packet Capture cli ##
```
capture *file* interface *interface* match *type protocol source IP destination IP*
```
ASA# capture capin interface inside match ip 10.0.0.0 255.255.255.0 192.168.0.0 255.255.255.0

ASA# show cap capin

ASA# no capture capin interface inside

 
ASA# capture capout interface outside match ip 10.0.0.0 255.255.255.0 172.1.1.0 255.255.255.0
ASA# no capture capout interface outside
ASA# show cap capout


Outut in format showing everything so can be copied
more system:running-config

