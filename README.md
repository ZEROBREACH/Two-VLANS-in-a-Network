# Two-VLANS-in-a-Network
Creating Two Vlans In a Network and each have Two Laptop In Them

# Step-by-Step Setup

# 1. Network Design
* VLAN 10: Laptops 1 & 2
* VLAN 20: Laptops 3 & 4
* Both VLANs connect to a switch → then to the router.
  <img width="745" height="352" alt="image" src="https://github.com/user-attachments/assets/16e269a6-a210-41af-b2cf-e69987a8ccfe" />

# 2. Assign VLANs on Switch

On the switch:
```
Switch> enable
Switch# configure terminal
Switch(config)# vlan 10
Switch(config-vlan)# name Sales
Switch(config-vlan)# exit
Switch(config)# vlan 20
Switch(config-vlan)# name HR
Switch(config-vlan)# exit
```
<img width="820" height="232" alt="image" src="https://github.com/user-attachments/assets/8d86ab56-6c40-4a30-af59-0fcc1cdcf51a" />

# 3. Assign Ports to VLANs

* Laptops 1 & 2 → VLAN 10 (say ports FastEthernet 0/1 and 0/2)
* Laptops 3 & 4 → VLAN 20 (say ports FastEthernet 0/3 and 0/4)
```
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
Switch(config-if)# exit
```
# 4. Configure Trunk Link to Router

Assume router is connected on fa0/24
```
Switch(config)# interface fa0/24
Switch(config-if)# switchport mode trunk
Switch(config-if)# exit
```
# 5. Configure Router (Router-on-a-Stick)

On router’s interface g0/0:
```
Router> enable
Router# configure terminal
Router(config)# interface g0/0.10
Router(config-subif)# encapsulation dot1Q 10
Router(config-subif)# ip address 192.168.10.1 255.255.255.0
Router(config-subif)# exit

Router(config)# interface g0/0.20
Router(config-subif)# encapsulation dot1Q 20
Router(config-subif)# ip address 192.168.20.1 255.255.255.0
Router(config-subif)# exit

Router(config)# interface g0/0
Router(config-if)# no shutdown
```
# 6. Assign IPs to Laptops

Laptop 1: 192.168.10.2 /24 , Gateway 192.168.10.1

Laptop 2: 192.168.10.3 /24 , Gateway 192.168.10.1

Laptop 3: 192.168.20.2 /24 , Gateway 192.168.20.1

Laptop 4: 192.168.20.3 /24 , Gateway 192.168.20.1

# 7. Verification

* Test within VLAN: ping between laptops in same VLAN.

* Test inter-VLAN: ping from a laptop in VLAN 10 to one in VLAN 20 → router should route between them.
