# VLAN

## Switch

### Switch to End device
```
switchport mode access
switchport access vlan 10
```

### Switch to Router
```
switchport mode trunk
switchport trunk allowed vlan 10
```

## Router
```
int g0/0.10
encapsulation dot1q 10
```

# DHCP
```
ip dhcp pool VLAN10
network 192.168.0.0 255.255.255.0
default-router 192.168.0.1
```

# Routing

## Static
*network, mask, next hop*
```
ip route 192.168.1.0 255.255.255.0 10.0.0.2
```

## OSPF
*network, inverted mask*
```
router ospf 1
network 192.168.0.0 0.0.0.255 area 0
```

# Passwords

## Enable
```
enable password kokos
```

## Console
```
line console 0
password kokos
login
```

## SSH
```
line vty 0 15
password kokos
login
```

## Encryption
```
service password encryption
```

# Access list
*source address, source inverted mask, destinaion address, destination inverted mask*
```
access-list 101 deny ip 192.168.0.0 0.0.0.255 192.168.1.0 0.0.0.255
access-list 101 permit ip any any
```
*in / out*
```
int g0/0
ip access-group 101 in
```

# Ether channel
```
int range fa0/1-4
channel-group 1 mode active
int port-channel 1
```

# Switchport security
```
switchport port-security
switchport port-security maximum 2
switchport port-security mac-address sticky
```
*protect / restrict / shutdown*
```
switchport port-security violation restrict
```

# Hot standby router
```
standby 1 ip 192.168.0.1
standby 1 priority 20
standby 1 preempt
```
