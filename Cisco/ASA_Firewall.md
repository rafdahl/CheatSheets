
GATHERING DATA TO MAKE A CHEATSHEET - - - IN PROGRESS


## ASA Packet Capture cli ##

***capture*** \<file name\> ***interface*** \<interface name\> ***match*** \<type protocol\> \<source IP\> \<destination IP\>
```
ASA# capture capin interface inside match ip 10.0.0.0 255.255.255.0 192.168.0.0 255.255.255.0
```
Display capture file
```
ASA# show cap capin
```
Delete the capture
```
ASA# no capture capin interface inside
```

***NOTE: OPTIONS***

***access-list:*** Capture packets that match access-list

***buffer:*** Default is 512kb but can go up to 32mb

***circular-buffer:*** Overwrite buffer when full

***headers-only:*** Capture only L2, L3 and L4

***real-time:*** Display in realtime, **BE CAREFULL** !!!!!!



Outut in format showing everything so can be copied
more system:running-config

