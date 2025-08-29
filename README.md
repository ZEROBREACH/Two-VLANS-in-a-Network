# Two-VLANS-in-a-Network
Creating Two Vlans In a Network and each have Two Laptop In Them

# Step-by-Step Setup

# 1. Network Design
* VLAN 10: Laptops 1 & 2
* VLAN 20: Laptops 3 & 4

# 2. Assign VLANs on Switch

On the switch:
```Switch> enable
Switch# configure terminal
Switch(config)# vlan 10
Switch(config-vlan)# name Sales
Switch(config-vlan)# exit

Switch(config)# vlan 20
Switch(config-vlan)# name HR
Switch(config-vlan)# exit```
