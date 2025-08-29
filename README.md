# Two-VLANS-in-a-Network
Creating Two Vlans In a Network and each have Two Laptop In Them

# Step-by-Step Setup

1. Network Design
* VLAN 10: Laptops 1 & 2
* VLAN 20: Laptops 3 & 4
 <img width="882" height="472" alt="image" src="https://github.com/user-attachments/assets/970bf6b8-355e-4631-86c8-14f8cd9b4abb" />
 
Both VLANs connect to a switch → then to the router.

2. Assign VLANs on Switch
On the switch:
Switch> enable
Switch# configure terminal
Switch(config)# vlan 10
Switch(config-vlan)# name Sales
Switch(config-vlan)# exit```

Switch(config)# vlan 20
Switch(config-vlan)# name HR
Switch(config-vlan)# exit```

<img width="525" height="177" alt="image" src="https://github.com/user-attachments/assets/1bdc8505-a402-4350-ae29-f0da84e74a14" />

# 3. Assign Ports to VLANs

* Laptops 1 & 2 → VLAN 10 (say ports FastEthernet 0/1 and 0/2)

* Laptops 3 & 4 → VLAN 20 (say ports FastEthernet 0/3 and 0/4)```
Switch(config)# interface fa0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
Switch(config-if)# exit
Switch(config)# interface fa0/2
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
Switch(config-if)# exit
Switch(config)# interface fa0/3
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 20
Switch(config-if)# exit
Switch(config)# interface fa0/4
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 20
Switch(config-if)# exit```

# 4. Configure Trunk Link to Router

Assume router is connected on fa0/24:

```Switch(config)# interface fa0/24
Switch(config-if)# switchport mode trunk
Switch(config-if)# exit```
